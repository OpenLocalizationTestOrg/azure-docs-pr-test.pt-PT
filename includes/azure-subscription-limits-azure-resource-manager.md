| Recurso | Limite Predefinido | Limite Máximo |
| --- | --- | --- |
| VMs por [subscrição](../articles/billing-buy-sign-up-azure-subscription.md) |10 000 <sup>1</sup> por Região |10 000 por Região |
| Total de núcleos de VM por [subscrição](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> por Região | Contactar o suporte |
| Núcleos de VM por série (Dv2, F, etc.) por [subscrição](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> por Região | Contactar o suporte |
| [Coadministradores](../articles/billing-add-change-azure-subscription-administrator.md) por subscrição |Ilimitado |Ilimitado |
| [Contas de armazenamento](../articles/storage/common/storage-create-storage-account.md) por subscrição |200 |200<sup>2</sup> |
| [Grupos de Recursos](../articles/azure-resource-manager/resource-group-overview.md) por subscrição |800 |800 |
| [Conjuntos de Disponibilidade](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) por subscrição |2000 por Região |2000 por Região |
| Leituras da API do Resource Manager |15 000 por hora |15 000 por hora |
| Escritas da API do Resource Manager |1200 por hora |1200 por hora |
| Tamanho do pedido da API do Resource Manager |4 194 304 bytes |4 194 304 bytes |
| Etiquetas por subscrição<sup>3</sup> |ilimitado |ilimitado |
| Cálculos de etiquetas únicas por subscrição<sup>3</sup> | 10,000 | 10,000 |
| [Serviços cloud](../articles/cloud-services/cloud-services-choose-me.md) por subscrição |Não Aplicável<sup>4</sup> |Não Aplicável<sup>4</sup> |
| [Grupos de afinidade](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) por subscrição |Não Aplicável<sup>4</sup> |Não Aplicável<sup>4</sup> |

<sup>1</sup>Os limites predefinidos variam consoante o Tipo de Categoria da oferta, como Avaliação Gratuita, Pay As You Go e série, como Dv2, F, G, etc.

<sup>2</sup>Isto inclui as contas de armazenamento Standard e Premium. Se necessitar de mais de 200 contas de armazenamento, efetue um pedido através do [Suporte do Azure](https://azure.microsoft.com/support/faq/). equipa de armazenamento do Azure Olá irá consultar o seu cenário de negócio e pode aprovar segurança too250 contas de armazenamento.

<sup>3</sup>Pode aplicar um número ilimitado de etiquetas por subscrição. número de Olá de sinalizadores por recurso ou grupo de recursos é too15 limitado. Gestor de recursos só devolve um [lista de nomes de etiqueta única e valores](/rest/api/resources/tags#Tags_List) na subscrição Olá quando o número de Olá de etiquetas é 10 000 ou inferior. No entanto, pode ainda localizar um recurso por tag quando excede o número de Olá 10 000.  

<sup>4</sup>estas funcionalidades já não são necessárias com grupos de recursos do Azure e Olá do Azure Resource Manager.

> [!NOTE]
> É importante tooemphasize que núcleos de máquina virtual tem um limite total regional, bem como um regionais por limite de séries (Dv2, F, etc.) de tamanho que são impostas em separado.  Por exemplo, considere uma subscrição com um limite total de núcleos de VM na região EUA Leste de 30, um limite de núcleos de série A de 30 e um limite de núcleos de série D de 30.  Esta subscrição será permitida toodeploy 30 A1 VMs ou 30 D1 VMs ou uma combinação de Olá dois tooexceed um total de 30 núcleos (por exemplo, 10 A1 VMs e 20 D1 VMs).  
> <!-- -->
> 
> 

