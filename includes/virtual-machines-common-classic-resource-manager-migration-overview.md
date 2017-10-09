# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Plataforma suportada a migração de recursos IaaS do clássico tooAzure Resource Manager
Neste artigo, vamos descrevem como podemos está a ativar a migração da infraestrutura como um recursos de serviço (IaaS) a partir de modelos de implementação do Gestor de tooResource do Olá clássico. Pode ler mais sobre [funcionalidades do Azure Resource Manager e os benefícios](../articles/azure-resource-manager/resource-group-overview.md). Iremos detalhe como gateways de site para site de rede tooconnect recursos de Olá dois modelos de implementação que coexistir na sua subscrição utilizando virtual.

## <a name="goal-for-migration"></a>Objetivo para migração
Gestor de recursos permite implementar aplicações complexas através de modelos, configura a máquinas virtuais utilizando extensões VM e incorpora a gestão de acesso e a etiquetagem. O Azure Resource Manager inclui implementação paralela, dimensionável para máquinas virtuais em conjuntos de disponibilidade. novo modelo de implementação Olá também fornece gestão de ciclo de vida de computação, rede e armazenamento separadamente. Por fim, há um foco sobre como ativar a segurança por predefinição com a imposição de Olá de máquinas virtuais numa rede virtual.

Quase todas as funcionalidades de Olá do modelo de implementação clássica Olá são suportadas para computação, rede e armazenamento no Gestor de recursos do Azure. toobenefit de Olá as novas capacidades no Gestor de recursos do Azure, pode migrar existente implementações do modelo de implementação clássica Olá.

## <a name="supported-resources-for-migration"></a>Recursos suportados para migração
Estes recursos IaaS clássicos são suportados durante a migração

* Virtual Machines
* Conjuntos de Disponibilidade
* Serviços Cloud
* Contas de Armazenamento
* Redes Virtuais
* Gateways de VPN
* Express Route Gateways _(no Olá mesma subscrição que a rede Virtual apenas)_
* Grupos de Segurança de Rede 
* Tabelas de Rota 
* IPs Reservados 

## <a name="supported-scopes-of-migration"></a>Suportado âmbitos de migração
Existem 4 diferentes formas toocomplete migração de recursos de computação, rede e armazenamento. Estes são 

* Migração de máquinas virtuais (não numa rede virtual)
* Migração de máquinas virtuais (numa rede virtual)
* Migração de contas de armazenamento
* Recursos desanexados (grupos de segurança de rede, as tabelas de rotas & IPs reservados)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migração de máquinas virtuais (não numa rede virtual)
Modelo de implementação do Resource Manager Olá, segurança é imposta para as suas aplicações por predefinição. Todas as VMs têm toobe numa rede virtual no modelo do Resource Manager Olá. Olá reinícios de plataforma do Azure (`Stop`, `Deallocate`, e `Start`) Olá VMs como parte da migração de Olá. Tem duas opções para redes virtuais Olá que Olá máquinas virtuais serão migradas para:

* Pode pedir Olá plataforma toocreate uma nova rede virtual e migrar a máquina virtual de Olá para nova rede virtual Olá.
* É possível migrar a máquina virtual de Olá numa rede virtual existente no Gestor de recursos.

> [!NOTE]
> Este âmbito da migração, ambos Olá operações de gestão plane em operações de dados-plane Olá poderão não ser permitidas para um período de tempo durante a migração de Olá.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migração de máquinas virtuais (numa rede virtual)
Para a maioria das configurações de VM, apenas os metadados de Olá está a migrar entre os modelos de implementação clássica e Resource Manager Olá. Olá subjacentes VMs estão em execução no Olá mesmo hardware, no Olá mesmo de rede e com Olá mesmo armazenamento. operações de gestão plane Olá poderão não ser permitidas para um determinado período de tempo durante a migração de Olá. No entanto, plane de dados de Olá continua toowork. Ou seja, as aplicações em execução em VMs (clássica) não cobrado um período de indisponibilidade durante a migração de Olá.

Olá seguintes configurações não é atualmente suportada. Se for adicionado suporte no futuro Olá, algumas VMs nesta configuração podem implicar o período de inatividade (aceda através de parar, Desalocação e reiniciar as operações de VM).

* Tiver mais do que um conjunto de disponibilidade num serviço em nuvem único.
* Tem um ou mais conjuntos de disponibilidade e VMs que não estão a ser um conjunto de disponibilidade num serviço em nuvem único.

> [!NOTE]
> Este âmbito da migração, plane de gestão de Olá pode não ser permitido para um período de tempo durante a migração de Olá. Para determinados configurações, tal como descrito anteriormente, dados plane período de indisponibilidade ocorre.
>
>

### <a name="storage-accounts-migration"></a>Migração de contas de armazenamento
migração totalmente integrada de tooallow, pode implementar as VMs do Gestor de recursos numa conta de armazenamento clássico. Com esta capacidade, recursos de rede e computação podem e devem ser migrados independentemente das contas de armazenamento. Depois de migrar sobre as máquinas virtuais e a rede Virtual, terá de toomigrate durante o processo de migração do armazenamento contas toocomplete Olá.

> [!NOTE]
> modelo de implementação do Resource Manager Olá não tem o conceito de Olá de clássico imagens e os discos. Quando a conta de armazenamento de Olá é migradas, clássicas imagens e os discos não são visíveis na pilha do Resource Manager Olá mas Olá fazer uma cópia de VHDs permanecem na conta do storage Olá.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Recursos desanexados (grupos de segurança de rede, as tabelas de rotas & IPs reservados)
Grupos de segurança de rede, as tabelas de rotas & IPs reservados que não estão anexados tooany máquinas virtuais e redes virtuais podem ser migradas de forma independente.

<br>

## <a name="unsupported-features-and-configurations"></a>Configurações e funcionalidades não suportadas
Iremos suporta atualmente algumas funcionalidades e configurações. Olá seguintes secções descreve o nosso recomendações em torno deles.

### <a name="unsupported-features"></a>Funcionalidades não suportadas
Olá seguintes funcionalidades não é atualmente suportada. Pode, opcionalmente, remova estas definições, migrar VMs Olá e, em seguida, volte a ativar as definições de Olá no modelo de implementação do Resource Manager Olá.

| Fornecedor de recursos | Funcionalidade | Recomendação |
| --- | --- | --- |
| Computação |Discos não associadas máquina virtual. | os blobs VHD Olá atrás destes discos serão obter migrados quando é migrada Olá conta de armazenamento |
| Computação |Imagens da máquina virtual. | os blobs VHD Olá atrás destes discos serão obter migrados quando é migrada Olá conta de armazenamento |
| Rede |ACLs de ponto final. | Remova as ACLs de ponto final e repita a migração. |
| Rede |Rede virtual com o Gateway do ExpressRoute e Gateway de VPN  | Remover Olá Gateway de VPN antes de iniciar a migração e, em seguida, recrie Olá VPN Gateway após a conclusão da migração. Saiba mais sobre [ExpressRoute migração](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Rede |ExpressRoute com ligações de autorização  | Remover a ligação de rede do Olá ExpressRoute circuito toovirtaul antes de iniciar a migração e, em seguida, recrie a ligação de Olá após a conclusão da migração. Saiba mais sobre [ExpressRoute migração](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Rede |Gateway de Aplicação | Remover Olá Gateway de aplicação antes de iniciar a migração e, em seguida, recrie Olá Gateway de aplicação depois de concluída a migração. |
| Rede |Redes virtuais utilizando o VNet Peering. | Migrar a rede Virtual tooResource Manager, em seguida, ponto. Saiba mais sobre [VNet Peering](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Configurações não suportadas
Olá seguintes configurações não é atualmente suportada.

| Serviço | Configuração | Recomendação |
| --- | --- | --- |
| Resource Manager |Função de acesso baseado em controlo (RBAC) para os recursos clássicos |Porque está modificado Olá URI de recursos de Olá após a migração, é recomendado que planeia atualizações de políticas RBAC Olá que necessitam de toohappen após a migração. |
| Computação |Associado uma VM de várias sub-redes |Atualize Olá sub-rede configuração tooreference apenas sub-redes. |
| Computação |Máquinas virtuais que pertencem a rede virtual tooa mas não tem uma sub-rede explícita atribuída |Opcionalmente, pode eliminar Olá VM. |
| Computação |Máquinas virtuais que possuem alertas, políticas de dimensionamento automático |migração de Olá atravessa e estas definições são ignoradas. Recomenda-se vivamente que, de avaliar o seu ambiente antes de Olá migração. Em alternativa, pode reconfigurar as definições de alerta de Olá após a conclusão da migração. |
| Computação |Extensões de VM de XML (BGInfo 1.*, depurador do Visual Studio, Web Deploy e depuração remota) |Não é suportada. Recomenda-se que remova estas extensões da migração de toocontinue Olá máquina virtual ou estes serão removidos automaticamente durante o processo de migração de Olá. |
| Computação |Diagnóstico de arranque com o armazenamento Premium |Desative a funcionalidade de diagnóstico de arranque para Olá VMs antes de continuar com a migração. Pode reativar o diagnóstico de arranque na pilha do Resource Manager Olá após a conclusão da migração de Olá. Além disso, os blobs que estão a ser utilizados para captura de ecrã e registos de série devem ser eliminados pelo que já não são cobradas para os blobs. |
| Computação |Serviços em nuvem que contêm funções da web/trabalho |Isto não é atualmente suportado. |
| Rede |Redes virtuais que contêm máquinas virtuais e funções da web/trabalho |Isto não é atualmente suportado. |
| Serviço de Aplicações do Azure |Redes virtuais que contêm os ambientes do App Service |Isto não é atualmente suportado. |
| O Azure HDInsight |Redes virtuais que contêm serviços do HDInsight |Isto não é atualmente suportado. |
| Serviços de ciclo de vida do Microsoft Dynamics |Redes virtuais que contêm máquinas virtuais que são geridas pelos serviços de ciclo de vida de Dynamics |Isto não é atualmente suportado. |
| Azure AD Domain Services |Redes virtuais que contêm os serviços de domínio do Azure AD |Isto não é atualmente suportado. |
| Azure RemoteApp |Redes virtuais que contenham implementações de Azure RemoteApp |Isto não é atualmente suportado. |
| API Management do Azure |Redes virtuais que contenham implementações de API Management do Azure |Isto não é atualmente suportado. Olá toomigrate IaaS VNET, altere Olá VNET de Olá implementação de API Management, que não é uma operação nenhum período de indisponibilidade. |
| Computação |Extensões de centro de segurança do Azure com uma VNET com um gateway de VPN na conectividade de trânsito ou gateway do ExpressRoute com o servidor DNS no local |Centro de segurança do Azure instala extensões no seu toomonitor de máquinas virtuais a segurança dos mesmos e emitir alertas automaticamente. Estas extensões, normalmente, obterem instaladas automaticamente se Olá política do Centro de segurança do Azure está ativada na subscrição Olá. A migração de gateway do ExpressRoute não é atualmente suportada e gateways de VPN com conectividade de trânsito perder o acesso no local. Eliminar ExpressRoute gateway ou migrar gateway VPN com conectividade de trânsito faz com que internet acesso tooVM armazenamento conta toobe perdido quando prosseguir com a consolidar migração Olá. não irá continuar a migração de Olá quando isto acontece porque não é possível povoar o blob de estado de agente de convidados Olá. É recomendado toodisable política do Centro de segurança do Azure na subscrição Olá 3 horas antes de continuar com a migração. |

