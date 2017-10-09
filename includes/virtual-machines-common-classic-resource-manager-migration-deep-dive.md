## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Significado da migração de recursos IaaS do tooResource de modelo de implementação clássica Olá Manager
Antes de iremos desagregar os detalhes de Olá, vamos ver a diferença de Olá entre operações plane de dados e gestão plane nos recursos de IaaS Olá.

* *Plane gestão/controlo* descreve chamadas de Olá que entrem em plane de gestão/controlo Olá ou Olá API para modificar os recursos. Por exemplo, operações como criar uma VM, reiniciar uma VM e atualizar de uma rede virtual com uma nova sub-rede gerir Olá com recursos. Diretamente não afetam a ligação toohello instâncias.
* *Plane dados* (aplicação) descreve Olá tempo de execução da aplicação Olá próprio e envolve a interação com as instâncias que não passam pelo Olá API do Azure. Por exemplo, o acesso ao seu Web site ou a extração de dados de uma instância do SQL Server ou um servidor MongoDB em execução são consideradas interações de planos de dados ou aplicação. Copiar um blob de uma conta de armazenamento e aceder a um público tooRDP de endereço IP ou SSH na máquina virtual de Olá também são plane de dados. Estas operações manter aplicação Olá em execução em toda a computação, redes e armazenamento.

Em segundo plano do Olá, plane de dados de Olá é Olá mesmo entre Olá modelo de implementação clássica e Resource Manager pilha. Durante o processo de migração, iremos traduzir representação Olá dos recursos de Olá de Olá toothat na modelo de implementação clássica na pilha do Resource Manager Olá. Como resultado, terá de toouse novas ferramentas, APIs, SDKs toomanage os recursos na pilha do Resource Manager Olá.

![Captura de ecrã que ilustra a diferença entre o plano de gestão/controlo e o plano de dados](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> Em alguns cenários de migração, Olá deixa de plataforma do Azure, deallocates e reiniciar as máquinas virtuais. Isto implica um curto período de indisponibilidade do plano de dados.
>

## <a name="hello-migration-experience"></a>experiência de migração de Olá
Antes de começar a experiência de migração de Olá, recomenda-se seguinte Olá:

* Certifique-se de que os recursos de Olá que pretende que o toomigrate não utilizar qualquer funcionalidades não suportadas ou configurações. Normalmente, a plataforma de Olá Deteta estes problemas e gera um erro.
* Se tiver VMs que não estão numa rede virtual, irá ser interrompidas e desalocadas como parte da Olá preparar a operação. Se não quiser que o endereço IP público do toolose Olá, procure para reservar o endereço IP Olá antes de acionar Olá preparar a operação. No entanto, se forem Olá VMs numa rede virtual, não estão parados e desalocadas.
* Planear a migração durante o horário de expediente tooaccommodate para quaisquer falhas inesperadas que poderão ocorrer durante a migração.
* Transferir a configuração atual do Olá das suas VMs utilizando o PowerShell, os comandos de interface de linha de comandos (CLI) ou toomake de REST APIs mais fácil para validação após Olá preparar passo é concluído.
* Atualize o modelo de implementação do automatização/operationalization scripts toohandle Olá Resource Manager antes de começar a migração de Olá. Opcionalmente, pode efetuar operações GET quando os recursos de Olá estão no Olá preparado estado.
* Avalie as políticas do Olá RBAC que estão configuradas em recursos de IaaS clássicos Olá e planear após a conclusão da migração de Olá.

fluxo de trabalho de migração de Olá é o seguinte

![Captura de ecrã que mostra o fluxo de trabalho de migração de Olá](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Todas as operações de Olá descritas Olá secções a seguir são idempotent. Se tiver um problema que não seja uma funcionalidade não suportada ou um erro de configuração, é recomendado que repita Olá preparar, abortar ou consolidar a operação. Olá plataforma Azure tenta novamente a ação de Olá.
>
>

### <a name="validate"></a>Validação
Olá validar a operação é Olá primeiro passo no processo de migração de Olá. objetivo de Olá deste passo é o estado de Olá tooanalyze dos recursos de Olá desejar toomigrate no modelo de implementação clássica Olá e devolver êxito/falha se recursos Olá são capazes de migração.

Selecionar uma rede virtual Olá ou um serviço em nuvem (se não estiver numa rede virtual) que pretende que toovalidate para migração.

* Se o recurso de Olá não for capaz de migração, Olá plataforma Azure apresenta uma lista de todos os motivos Olá por que motivo não é suportada para migração.

#### <a name="checks-not-done-in-validate"></a>Não é efetuadas na validar as verificações

Validar operação analisa apenas o estado de Olá dos recursos de Olá no modelo de implementação clássica Olá. Pode verificar a para todas as falhas e cenários não suportados devido a configurações de toovarious no modelo de implementação clássica Olá. Não é possível toocheck para todos os problemas que hello do Azure Resource Manager pilha poderá impõe nos recursos de Olá durante a migração. Estes problemas são verificados apenas quando os recursos de Olá são submetidos a transformação no passo seguinte Olá da migração, ou seja, preparar. tabela de Olá abaixo apresenta uma lista de todos os problemas de Olá não verificados validar.


|Verificações de redes não está no validar|
|-|
|Uma rede Virtual ter ER e VPN gateways|
|Desligar a ligação de gateway de rede virtual no Estado|
|Todos os circuitos de ER estão pilha do Resource Manager tooAzure pré-migrados|
|Quota de Gestor de recursos do Azure verifica a existência de recursos de rede, ou seja, um IP público estático, os IPs públicos dinâmicos, Balanceador de carga, grupos de segurança de rede, as tabelas de rotas, Interfaces de rede |
| Verifique se todas as regras de Balanceador de carga são válidas em implementação/VNET |
| Verifique a existência de IPs privados em conflito entre as VMs desalocada de paragem na Olá mesmo VNET |

### <a name="prepare"></a>Preparação
Olá preparar a operação é o segundo passo de Olá no processo de migração de Olá. objetivo deste passo Olá transformação de Olá toosimulate de Olá recursos IaaS de implementação clássica modelo tooResource do Gestor de recursos e apresenta esta lado para lhe toovisualize.

> [!NOTE] 
> Os recursos de clássico não são modificados durante este passo. Se um passo seguro toorun se estiver a tentar terminar a migração. 

Selecionar Olá virtual rede ou Olá serviço em nuvem (se não se trata de uma rede virtual) que pretende que tooprepare para migração.

* Se o recurso de Olá não for capaz de migração, Olá plataforma Azure interrompe o processo de migração de Olá e apresenta uma lista de razão Olá por que motivo Olá preparar a operação falhou.
* Se o recurso de Olá for capaz de migração, Olá plataforma Azure bloqueia primeiro baixo operações de gestão plane Olá para recursos Olá em migração. Por exemplo, não é possível tooadd um tooa de disco de dados VM em migração.

Olá plataforma do Azure, em seguida, inicia Olá migração dos metadados de implementação clássica modelo tooResource gestor para Olá migrar os recursos.

Depois de preparar Olá operação foi concluída, tem Olá opção de visualizar recursos Olá no modelo de implementação clássica e Resource Manager. Para cada serviço em nuvem no modelo de implementação clássica Olá, hello plataforma do Azure cria um nome de grupo de recursos com o padrão de Olá `cloud-service-name>-Migrated`.

> [!NOTE]
> Não é possível tooselect nome de Olá do grupo de recursos criado para os recursos migrados (ou seja, "-migrados"), mas após a conclusão da migração, pode utilizar o Azure Resource Manager mover funcionalidade toomove recursos tooany grupo de recursos que pretende. mais informações sobre esta Consulte tooread [mover grupo de recursos de toonew de recursos ou subscrição](../articles/resource-group-move-resources.md)

Seguem-se dois ecrãs que mostram o resultado de Olá após um operação de preparação de efetuado com êxito. Primeiro ecrã mostra um grupo de recursos que contém o serviço de nuvem Olá original. Segundo ecrã mostra Olá novo "-migrados" grupo de recursos contém recursos da Olá equivalente do Azure Resource Manager.

![Captura de ecrã que mostra o serviço cloud clássico do portal](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Captura de ecrã que mostra recursos do Azure Resource Manager em Preparação no Portal](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Segue-se em segundo plano ver os recursos após a conclusão de Olá da fase de preparação. Note que o recurso de Olá é plane de dados de Olá é Olá mesmo. Este é representado na plane de gestão de Olá (modelo de implementação clássica) e plane de controlo de Olá (Resource Manager).

![Em segundo plano de Olá na fase preparar](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Máquinas virtuais que não estão numa rede Virtual clássica são parado-desalocada nesta fase da migração.
>

### <a name="check-manual-or-scripted"></a>Verificação (manual ou com script)
No passo de verificação Olá, opcionalmente, pode utilizar configuração Olá que transferiu anteriormente toovalidate que migração Olá procura correta. Em alternativa, pode iniciar sessão toohello portal e verificação lugar para cima Olá propriedades e recursos toovalidate que procura boa migração de metadados.

Se estiver a migrar uma rede virtual, a maioria das configurações de máquinas virtuais não são reiniciadas. Para aplicações nessas VMs, pode validar que aplicação Olá ainda se encontra em execução.

Pode testar a monitorização/automatização e os scripts operacional toosee se Olá VMs está a funcionar conforme esperado e se os scripts atualizados funcionem corretamente. Apenas GET operações são suportadas quando os recursos de Olá estão numa Olá preparado estado.

Não há nenhuma janela de tempo definido antes de que necessita de migração de Olá toocommit. Pode permanecer neste estado o tempo que quiser. No entanto, plane de gestão de Olá está bloqueada para estes recursos, até que a abortar ou consolidar.

Se vir quaisquer problemas, pode abortar migração Olá e voltar atrás toohello modelo de implementação clássica. Depois de voltar atrás, Olá plataforma Azure abrirá operações de gestão plane Olá nos recursos de Olá, de modo a que possa retomar as operações normais nessas VMs no modelo de implementação clássica Olá.

### <a name="abort"></a>Abortar
Abortar passo é opcional que pode utilizar o seu modelo de implementação clássica toohello alterações toorevert e parar a migração de Olá. Esta operação elimina Olá metadados de Gestor de recursos para os seus recursos que foi criado no passo de preparação anterior Olá. 

![Em segundo plano de Olá na fase abortar](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Não é possível executar esta operação depois de ter ativada a operação de consolidação Olá.     
>

### <a name="commit"></a>Consolidação
Depois de concluir a validação de Olá, pode confirmar migração Olá. Recursos não serão apresentados já no modelo de implementação clássica e só estão disponíveis no modelo de implementação do Resource Manager Olá. Olá recursos migrados podem ser geridos apenas no portal Olá de novo.

> [!NOTE]
> Esta é uma operação idempotent. Se falhar, recomenda-se a repetir a operação de Olá. Se as prossegue toofail, crie um pedido de suporte ou crie um fórum post com uma etiqueta de ClassicIaaSMigration no nosso [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Em segundo plano de Olá na fase consolidar](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Onde toobegin migração?

Eis uma fluxograma que mostra como tooproceed com a migração

![Captura de ecrã que mostra os passos de migração de Olá](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Tradução de recursos de Gestor de recursos de tooAzure de modelo de implementação clássica
Pode encontrar o modelo de implementação clássica Olá e representações de Gestor de recursos dos recursos de Olá no Olá a tabela seguinte. Atualmente, não são suportadas outras funcionalidades e recursos.

| Representação clássica | Representação do Resource Manager | Notas detalhadas |
| --- | --- | --- |
| Nome do serviço cloud |Nome DNS |Durante a migração, é criado um novo grupo de recursos para cada serviço em nuvem com o padrão de nomenclatura de Olá `<cloudservicename>-migrated`. Este grupo de recursos contém todos os seus recursos. nome do serviço de nuvem de Olá torna-se um nome DNS que estão associado com o endereço IP público Olá. |
| Máquina virtual |Máquina virtual |As propriedades específicas de cada VM são migradas sem alterações. Determinadas informações de osProfile, como o nome do computador, não são armazenadas no modelo de implementação clássica Olá e permanecem vazias após a migração. |
| Recursos de disco ligado tooVM |Os discos ligados implícitas tooVM |Discos não estão modelados como recursos de nível superior no modelo de implementação do Resource Manager Olá. São migrados como discos implícitos em Olá VM. Apenas os discos que estão anexados tooa VM são atualmente suportadas. VMs do Gestor de recursos pode agora utilizar contas de armazenamento clássicas, que lhe permite facilmente migrados Olá discos toobe sem quaisquer atualizações. |
| Extensões de VM |Extensões de VM |Todas as extensões de recursos de Olá, exceto as extensões XML, são migradas a partir do modelo de implementação clássica Olá. |
| Certificados de máquinas virtuais |Certificados no Azure Key Vault |Se um serviço em nuvem contém os certificados de serviço, um novo cofre de chaves do Azure por serviço em nuvem e move-certificados Olá no Cofre de chaves Olá. Olá VMs são certificados de Olá tooreference atualizado do Cofre de chaves Olá. <br><br> **Nota:** não elimine Olá keyvault como pode causar Olá VM toogo num Estado com falhas. Estamos a trabalhar em melhorar coisas no back-end de Olá, para que possa ser eliminado em segurança ou movida, juntamente com Olá nova subscrição de VM tooa cofres de chave. |
| Configuração WinRM |Configuração WinRM em osProfile |Não altere é movida a configuração da gestão remota do Windows, como parte da migração de Olá. |
| Propriedade Availability-set |Recurso Availability-set | Especificação de conjunto de disponibilidade foi uma propriedade no Olá VM no modelo de implementação clássica Olá. Conjuntos de disponibilidade tornar-se um recurso de nível superior como parte da migração de Olá. Olá configurações seguintes não são suportadas: vários conjuntos de disponibilidade por serviço em nuvem ou conjuntos de disponibilidade de um ou mais juntamente com as VMs que não estejam em qualquer conjunto de disponibilidade num serviço em nuvem. |
| Configuração de rede numa VM |Interface de rede primária |Configuração de rede numa VM é representada como recurso de interface de rede principal Olá após a migração. Para as VMs que não estão na rede virtual, Olá internas alterações do endereço IP durante a migração. |
| Várias interfaces de rede numa VM |Interfaces de rede |Se uma VM tem várias interfaces de rede associadas, cada interface de rede torna-se um recurso de nível superior como parte da migração de Olá no modelo de implementação do Resource Manager Olá, juntamente com todas as propriedades de Olá. |
| Conjunto de pontos finais com balanceamento de carga |Load balancer |No modelo de implementação clássica Olá, plataforma Olá atribuído um balanceador de carga implícito para cada serviço em nuvem. Durante a migração, é criado um novo recurso de Balanceador de carga e conjunto de ponto final de balanceamento de carga Olá torna-se as regras de Balanceador de carga. |
| Regras NAT de entrada |Regras NAT de entrada |Pontos finais de entrada definidos no Olá VM são regras tradução de endereços de rede do tooinbound convertida Balanceador de carga Olá durante a migração de Olá. |
| Endereço VIP |Endereço IP público com o nome DNS |endereço IP virtual Olá torna-se de um endereço IP público e está associado ao balanceador de carga Olá. Um IP virtual só pode ser migrado se existir um ponto final de entrada atribuído tooit. |
| Rede virtual |Rede virtual |rede virtual Olá é migrada, com todas as respetivas propriedades, modelo de implementação do Resource Manager toohello. É criado um novo grupo de recursos com o nome de Olá `-migrated`. |
| IPs Reservados |Endereço IP público com o método de alocação estática |IPs reservados associados com Balanceador de carga Olá são migradas juntamente com a migração de Olá do serviço de nuvem Olá ou Olá numa máquina virtual. Atualmente, não é suportada a migração de IPs reservados. |
| Endereço IP público por VM |Endereço IP público com o método de alocação dinâmica |Olá endereço IP público associado Olá que VM é convertida como um recurso de endereço IP público, com toostatic de conjunto de método de alocação de Olá. |
| NSGs |NSGs |Grupos de segurança de rede associados a uma sub-rede são clonados como parte do modelo de implementação do Olá migração toohello Resource Manager. Olá NSG no modelo de implementação clássica Olá não é removido durante a migração de Olá. No entanto, as operações de gestão plane Olá para Olá NSG estão bloqueadas durante a migração de Olá está em curso. |
| Servidores DNS |Servidores DNS |Servidores DNS associados a uma rede virtual ou Olá VM são migradas como parte da Olá correspondente migração de recursos, juntamente com todas as propriedades de Olá. |
| UDRs |UDRs |As rotas definidas pelo utilizador associadas uma sub-rede são Clonadas como parte do modelo de implementação do Olá migração toohello Resource Manager. Olá UDR no modelo de implementação clássica Olá não é removido durante a migração de Olá. operações de gestão plane Olá para Olá UDR estão bloqueadas durante a migração de Olá está em curso. |
| Propriedade de reencaminhamento de IPs na configuração de rede de uma VM |IP reencaminhamento propriedade Olá NIC |propriedade de reencaminhamento IP Olá numa VM é propriedade de tooa convertida na interface de rede Olá durante a migração de Olá. |
| Balanceador de carga com vários IPs |Balanceador de carga com vários recursos de IP público |Cada IP público associado com Balanceador de carga Olá é convertida tooa recurso de IP público e associou com Balanceador de carga Olá após a migração. |
| Nomes DNS internos no Olá VM |Nomes DNS internos no Olá NIC |Durante a migração, sufixos DNS internos Olá para VMs Olá são propriedade de só de leitura do tooa migrados com o nome "InternalDomainNameSuffix" Olá NIC. sufixo Olá permanece inalterado após a migração e resolução VM deve continuar toowork como anteriormente. |
| Gateway de Rede Virtual |Gateway de Rede Virtual |As propriedades do Gateway de Rede Virtual são migradas sem alterações. Olá VIP associado a gateway Olá não altera nenhum. |
| Site de rede local |Gateway de Rede Local |Propriedades do site de rede local são migrados tooa inalterados novo recurso designado por Gateway de rede Local. Este representa os prefixos de endereços no local e o IP do gateway remoto. |
| Referências de ligações |Ligação |As referências de conectividade entre o gateway e o site de rede local na configuração de rede são representadas por um recurso criado recentemente, com o nome ligação, no Resource Manager após a migração. Todas as propriedades de referência de conectividade nos ficheiros de configuração de rede são copiados toohello inalterados recém-criado recurso de ligação. VNet tooVNet conectividade no clássico é conseguida através da criação de dois túneis IPsec toolocal locais de rede que representa Olá VNets. Este é transformada tooVnet2Vnet ligação tipo no modelo de Gestor de recursos sem necessidade de gateways de rede local. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>As alterações tooyour automatização e ferramentas após a migração
Como parte da migração os recursos do Olá modelo toohello Resource Manager implementação modelo de implementação clássica, terá de tooupdate a automatização existente ou tooensure ferramentas que continua a toowork após a migração de Olá.
