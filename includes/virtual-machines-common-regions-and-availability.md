# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiões e disponibilidade para máquinas virtuais no Azure
O Azure funciona em vários datacenters em todo o mundo. Estes datacenters são agrupados por regiões geográficas, dando-lhe a flexibilidade de escolher onde pretende criar as suas aplicações. É importante compreender como e onde as suas máquinas virtuais (VMs) funcionam no Azure, juntamente com as opções para maximizar o desempenho, a disponibilidade e a redundância. Este artigo fornece-lhe uma descrição geral das funcionalidades de disponibilidade e redundância do Azure.

## <a name="what-are-azure-regions"></a>O que são as regiões do Azure?
Criar recursos do Azure em regiões geográficas definidas como 'EUA oeste', 'Europa do Norte' ou 'Sudeste Asiático'. Pode rever a [lista de regiões e as respetivas localizações](https://azure.microsoft.com/regions/). Dentro de cada região, existem vários datacenters para fornecer redundância e disponibilidade. Esta abordagem proporciona flexibilidade ao conceber aplicações para criar VMs mais próximo para os seus utilizadores e para cumprir quaisquer legal, compatibilidade ou fiscais fins.

## <a name="special-azure-regions"></a>Regiões do Azure especiais
O Azure tem algumas regiões especiais que pretende utilizar ao criar o suas aplicações para fins legais ou de compatibilidade. Estas regiões especiais incluem:

* **Gov (US) - Virginia** e **Gov (US) - Iowa**
  * Uma instância isolada da rede física e lógica do Azure para agências e parceiros do governo dos Estados Unidos da América, operada por pessoas selecionadas dos EUA. Inclui certificações de conformidades adicionais, como [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) e [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Leia mais sobre o [Azure Government](https://azure.microsoft.com/features/gov/).
* **Leste da China** e **Norte da China**
  * Estas regiões estão disponíveis através de uma parceria exclusiva entre a Microsoft e a 21Vianet, nos termos da qual a Microsoft não controla diretamente os datacenters. Veja mais informações sobre o [Microsoft Azure na China](http://www.windowsazure.cn/).
* **Alemanha Central** e **Nordeste da Alemanha**
  * Estas regiões estão disponíveis através de um modelo de fidedigno de dados em dados de cliente permanecem na Alemanha sob o controlo de T-sistemas, uma empresa Deutsche Telekom, agir como o administrador de dados em alemão.

## <a name="region-pairs"></a>Pares de região
Cada região do Azure está emparelhada com outra região na mesma geografia (por exemplo, E.U.A., Europa ou Ásia). Esta abordagem permite a replicação dos recursos, como o armazenamento de VMs numa geografia, que deverá reduzir a probabilidade de desastres naturais, conflitos civis, falhas de energia ou falhas de rede física que afetem as duas regiões ao mesmo tempo. As vantagens adicionais de pares de região incluem:

* Em caso de uma maior indisponibilidade do Azure, uma região tem prioridade entre cada par, para ajudar a reduzir o tempo de restauro das aplicações. 
* As atualizações do Azure planeadas são lançadas para regiões emparelhadas, uma de cada vez, para minimizar o período de indisponibilidade e o risco de indisponibilidade de aplicação.
* Os dados continuam a residir na geografia do respetivo par (exceto para o Sul do Brasil), para efeitos fiscais e de aplicação da lei.

Os exemplos de pares de região incluem:

| Primária | Secundária |
|:--- |:--- |
| EUA Oeste |EUA Leste |
| Europa do Norte |Europa Ocidental |
| Sudeste Asiático |Ásia Oriental |

Pode ver a [lista completa de pares regionais aqui](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilidade de funcionalidades
Alguns serviços ou funcionalidades de VM só estão disponíveis em determinadas regiões, como VMs com tamanhos ou tipos de armazenamento específicos. Existem também alguns serviços globais do Azure que não requerem a seleção de uma região específica, como o [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Gestor de Tráfego](../articles/traffic-manager/traffic-manager-overview.md) ou [DNS do Azure](../articles/dns/dns-overview.md). Para ajudá-lo a estruturar o seu ambiente de aplicação, pode verificar a [disponibilidade dos serviços do Azure em cada região](https://azure.microsoft.com/regions/#services). Também pode [programaticamente consultar as restrições em cada região e tamanhos de VM suportados](../articles/azure-resource-manager/resource-manager-sku-not-available-errors.md).

## <a name="storage-availability"></a>Disponibilidade de armazenamento
Compreender as regiões e as geografias do Azure ganha importância ao considerar as opções de replicação de armazenamento disponíveis. Dependendo do tipo de armazenamento, existem opções de replicação diferentes.

**Managed Disks do Azure**
* Armazenamento localmente redundante (LRS)
  * Replica os dados três vezes na região em que criou a sua conta de armazenamento.

**Discos com base na conta de armazenamento**
* Armazenamento localmente redundante (LRS)
  * Replica os dados três vezes na região em que criou a sua conta de armazenamento.
* Armazenamento com redundância de zona (ZRS)
  * Replica os dados três vezes em dois ou três locais, numa única região ou em duas regiões.
* Armazenamento georredundante (GRS)
  * Replica os dados numa região secundária a centenas de quilómetros de distância da região primária.
* Armazenamento georredundante com acesso de leitura (RA-GRS)
  * Replica os dados numa região secundária, como acontece com o GRS, mas também fornece acesso só de leitura aos dados na localização secundária.

A tabela seguinte fornece uma descrição geral rápida das diferenças entre os tipos de replicação de armazenamento:

| Estratégia de replicação | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Os dados são replicados em vários locais. |Não |Sim |Sim |Sim |
| Os dados podem ser lidos a partir da localização secundária e da localização principal. |Não |Não |Não |Sim |
| Número de cópias dos dados mantidas em nós separados. |3 |3 |6 |6 |

Pode ler mais sobre as [opções de replicação de Armazenamento do Azure aqui](../articles/storage/common/storage-redundancy.md). Para mais informações sobre discos geridos, veja [Managed Disks Overview (Descrição geral dos Managed Disks)](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Custos de armazenamento
Os preços podem variar consoante o tipo de armazenamento e disponibilidade que selecionou.

**Managed Disks do Azure**
* Os discos geridos Premium são apoiados por unidades de Solid-State (SSDs) e discos geridos padrão são apoiados por discos girar regular. Os Managed Disks Premium e os Standard são carregados com base na capacidade de aprovisionamento do disco.

**Discos não geridos**
* Armazenamento Premium é copiado por Solid-State unidades (SSDs) e é cobrado com base na capacidade do disco.
* O armazenamento Standard está protegido por discos rotativos normais é cobrado com base na capacidade em utilização e na disponibilidade de armazenamento pretendida.
  * Para RA-GRS, existe uma cobrança adicional da Transferência de Dados de Georreplicação para a largura de banda da replicação desses dados para outra região do Azure.

Veja [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre os preços para tipos de armazenamento e opções de disponibilidade diferentes.

## <a name="availability-sets"></a>Conjuntos de disponibilidade
Um conjunto de disponibilidade é um agrupamento lógico de VMs num centro de dados que permite ao Azure compreender como a aplicação é criada para fornecer redundância e disponibilidade. Recomendamos que dois ou mais VMs são criadas dentro de um conjunto para fornecer uma aplicação altamente disponível e para cumprir os de disponibilidade de [99,95% SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Quando uma única VM estiver a utilizar o [Armazenamento Premium do Azure](../articles/virtual-machines/windows/premium-storage.md), o SLA do Azure aplica-se para eventos de manutenção não planeada. 

Um conjunto de disponibilidade é composto por dois agrupamentos adicionais que protegem contra falhas de hardware e permita que as atualizações possam ser aplicadas - falhas domínios (FDs) e domínios de atualização (UDs). Pode ler mais sobre como gerir a disponibilidade de [VMs do Linux](../articles/virtual-machines/linux/manage-availability.md) ou [VMs do Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domínios de falha
Um domínio de falha é um grupo lógico de hardware subjacente que partilha a mesma origem de energia e o mesmo comutador de rede física, semelhante a uma estrutura dentro de um datacenter no local. À medida que cria VMs num conjunto de disponibilidade, a plataforma Azure distribui automaticamente as suas VMs por estes domínios de falha. Esta abordagem limita o impacto de potenciais falhas de hardware físico, indisponibilidade de rede ou falhas de energia.

### <a name="update-domains"></a>Domínios de atualização
Um domínio de atualização é um grupo lógico de hardware subjacente que pode entrar em manutenção ou ser reiniciado ao mesmo tempo. À medida que cria VMs num conjunto de disponibilidade, a plataforma Azure distribui automaticamente as suas VMs por estes domínios de atualização. Esta abordagem garante que, pelo menos, uma instância da aplicação permanece sempre em execução quando a plataforma Azure entra em manutenção periódica. A ordem dos domínios de atualização que estão a ser reiniciados não pode continuar sequencialmente durante a manutenção planeada, sendo que apenas um domínio de atualização é reiniciado de cada vez.

### <a name="managed-disk-fault-domains"></a>Domínios de falhas de disco geridos
Para as VMs que utilizam os [Managed Disks do Azure](../articles/virtual-machines/windows/faq-for-disks.md), as VMs são alinhadas com domínios de falha de discos geridos ao utilizar um conjunto de disponibilidade gerido. Este alinhamento garante que todos os discos geridos ligados a uma VM estão dentro do mesmo domínio de falha do disco gerido. Apenas as VMs com discos geridos podem ser criadas num conjunto de disponibilidade gerido. O número de domínios de falha do disco gerido varia por região - dois ou três domínios de falha do disco gerido por região. Pode ler mais sobre estes geridos domínios de falhas de disco para [VMs com Linux](../articles/virtual-machines/linux/manage-availability.md?#use-managed-disks-for-vms-in-an-availability-set) ou [VMs do Windows](../articles/virtual-machines/linux/manage-availability.md?#use-managed-disks-for-vms-in-an-availability-set).

## <a name="availability-zones"></a>Zonas de disponibilidade

[Zonas de disponibilidade](../articles/availability-zones/az-overview.md) (pré-visualização), uma alternativa à disponibilidade define, expanda o nível de controlo tem de manter a disponibilidade das aplicações e dados nas suas VMs. Uma zona de disponibilidade é uma zona fisicamente separada dentro de uma região do Azure. Existem três zonas de disponibilidade por região do Azure suportada. Cada zona de disponibilidade tem um distintos origem, rede e arrefecimento de energia e são logicamente separados de outros zonas de disponibilidade na região do Azure. Por arquitetar as suas soluções para utilizar VMs replicadas em zonas, pode proteger as aplicações e dados da perda de um centro de dados. Se uma zona for comprometida, em seguida, replicadas aplicações e dados estão disponíveis de imediato noutra zona. 

![Zonas de disponibilidade](./media/virtual-machines-common-regions-and-availability/three-zones-per-region.png)

[!INCLUDE [availability-zones-preview-statement.md](availability-zones-preview-statement.md)]

Saiba mais sobre a implementação de um [Windows](../articles/virtual-machines/windows/create-powershell-availability-zone.md) ou [Linux](../articles/virtual-machines/linux/create-cli-availability-zone.md) VM com uma zona de disponibilidade.

## <a name="next-steps"></a>Passos seguintes
Pode agora começar a utilizar estas funcionalidades de redundância e disponibilidade para criar o seu ambiente do Azure. Para informações relativas a melhores práticas, veja [Melhores Práticas de Disponibilidade do Azure](../articles/best-practices-availability-checklist.md).

