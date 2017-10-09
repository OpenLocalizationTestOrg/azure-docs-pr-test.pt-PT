Máquinas virtuais do Azure (VMs), por vezes, poderá reiniciar por nenhum motivo aparente, sem provas do ter iniciada a operação de reinício de Olá. Este artigo apresenta uma lista de ações de Olá e os eventos que podem fazer com que as VMs tooreboot e fornece informações sobre como tooavoid inesperado reiniciar problemas ou reduzir o impacto de Olá esses problemas.

## <a name="configure-hello-vms-for-high-availability"></a>Configurar Olá VMs de elevada disponibilidade
Olá melhor forma tooprotect uma aplicação que está em execução no Azure contra VM reinicia e período de indisponibilidade é tooconfigure Olá VMs de elevada disponibilidade.

Este nível da aplicação de tooyour de redundância de tooprovide, recomendamos que agrupe duas ou mais VMs num conjunto de disponibilidade. Esta configuração assegura que durante a um evento de manutenção planeada ou, pelo menos uma VM está disponível e de que cumpre os Olá 99,95 percentagem [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Para obter mais informações sobre conjuntos de disponibilidade, consulte Olá seguintes artigos:

- [Gerir a disponibilidade de Olá de VMs](../articles/virtual-machines/windows/manage-availability.md)
- [Configurar a disponibilidade de VMs](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Informações de estado de funcionamento de recursos 
Estado de funcionamento de recursos do Azure é um serviço que expõe o estado de funcionamento de Olá de recursos do Azure individuais e fornece orientações acionável para resolução de problemas. Num ambiente de nuvem em que não está toodirectly possíveis servidores de acesso ou elementos de infraestrutura, objetivo Olá do Estado de funcionamento de recursos está na altura de Olá tooreduce que passam na resolução de problemas. Em particular, objetivo Olá está na altura de Olá tooreduce que passam a determinar se raiz Olá problema Olá situam-se na aplicação Olá ou num evento dentro Olá plataforma Azure. Para obter mais informações, consulte [compreender e utilizar o estado de funcionamento do recurso](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Ações e os eventos que podem causar Olá tooreboot VM

### <a name="planned-maintenance"></a>Manutenção planeada
Microsoft Azure executa periodicamente as atualizações em toda a fiabilidade do Olá globo tooimprove Olá, desempenho e segurança da infraestrutura de anfitrião de Olá subjacente a VMs. Muitas destas atualizações, incluindo atualizações preservação de memória, são efetuadas sem qualquer impacto nas suas VMs ou serviços em nuvem.

No entanto, algumas atualizações requerem um reinício. Nestes casos, Olá VMs são encerradas, mas iremos aplicar o patch infraestrutura Olá e, em seguida, Olá VMs são reiniciadas.

toounderstand é que a manutenção planeada do Azure e como-lo pode afetar a disponibilidade de Olá das suas VMs do Linux, consulte os artigos de Olá listados aqui. artigos de Olá fornecem fundo sobre o processo de manutenção planeada do Azure de Olá e como tooschedule planeada manutenção toofurther reduzir o impacto de Olá.

- [Manutenção planeada para VMs no Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Como tooschedule a manutenção planeada em VMs do Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Atualizações para preservação de memória   
Para esta classe de atualizações no Microsoft Azure, os utilizadores passam sem afetar as respetivas VMs em execução. Muitas destas atualizações são toocomponents ou serviços que podem ser atualizados sem interferir com Olá executar instância. Alguns são atualizações de infraestrutura da plataforma no sistema de operativo de anfitrião Olá que podem ser aplicados sem um reinício do Olá VMs.

Estas atualizações preservação de memória são realizadas com a tecnologia que permite a migração em direto no local. Quando está a ser atualizado, Olá VM é colocada num *colocada em pausa* estado. Este estado preserva memória RAM Olá enquanto o sistema de operativo de anfitrião subjacente Olá recebe atualizações necessárias Olá e correções de erros. Olá VM é retomado dentro de 30 segundos, de que está a ser colocada em pausa. Depois de Olá que VM é retomada, o relógio é automaticamente sincronizado.

Devido ao período de pausa curto Olá, implementar atualizações através destes mecanismo significativamente reduz o impacto Olá Olá VMs. No entanto, nem todas as atualizações podem ser implementadas desta forma. 

Atualizações de várias instâncias (para VMs num conjunto de disponibilidade) são aplicados um domínio de atualização de cada vez.

> [!NOTE]
> Máquinas de Linux que tenham versões antigas do kernel são afetadas por um panic kernel durante este método de atualização. tooavoid este problema, atualização tookernel versão 3.10.0-327.10.1 ou posterior. Para obter mais informações, consulte [uma VM do Linux do Azure num kernel baseado em 3.10 panics após uma atualização do nó de anfitrião](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Ações de reinício ou encerramento iniciadas pelo utilizador
 
Se efetuar um reinício de Olá portal do Azure, Azure PowerShell, a interface de linha de comandos ou repor API, para encontrar eventos de Olá Olá [registo de atividade do Azure](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Se efetuar a ação de Olá do sistema de operativo Olá da VM, pode encontrar eventos de Olá nos registos do sistema de Olá.

Outros cenários que normalmente causam Olá VM tooreboot incluem várias ações de alteração da configuração. Normalmente, irá ver uma mensagem de aviso que indica que a execução de uma ação específica resultará numa reinicialização Olá VM. Os exemplos incluem quaisquer operações de redimensionamento de VM, Olá palavra-passe da conta administrativa Olá a alteração e definir um endereço IP estático.

### <a name="azure-security-center-and-windows-update"></a>Centro de segurança do Azure e no Windows Update
Centro de segurança do Azure monitoriza diárias Windows e VMs com Linux para atualizações do sistema operativo em falta. Centro de segurança obtém uma lista de atualizações críticas e de segurança disponíveis do Windows Update ou Windows Server Update Services (WSUS), dependendo de que o serviço está configurado numa VM do Windows. Centro de segurança também verifica a existência de atualizações mais recentes do Olá para sistemas Linux. Se a VM está em falta uma atualização do sistema, o Centro de segurança recomenda se aplicam a atualizações do sistema. aplicação Olá destas atualizações do sistema é controlada através de Olá Centro de segurança no Olá portal do Azure. Depois de aplicar algumas atualizações, os reinícios VM poderão ser necessários. Para obter mais informações, consulte [aplicar atualizações do sistema no Centro de segurança do Azure](../articles/security-center/security-center-apply-system-updates.md).

Como servidores no local, Azure não push atualizações do Windows Update tooWindows VMs do Azure, uma vez que estas máquinas são toobe pretendido gerido pelo que os utilizadores. É, no entanto, encouraged tooleave Olá Windows Update definição automática ativada. Instalação automática de atualizações do Windows Update pode também fazer com que toooccur reinícios após Olá atualizações são aplicadas. Para obter mais informações, consulte [FAQ de atualização do Windows](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Noutras situações que afetam a disponibilidade de Olá da sua VM
Existem outros casos em que Azure poderá suspender ativamente utilize Olá de uma VM. Receberá notificações de e-mail antes desta ação é executada, pelo que terá um tooresolve hipótese Olá problemas subjacentes. Os exemplos dos problemas que afetam a disponibilidade VM incluem violações de segurança e de expiração de Olá dos métodos de pagamento.

### <a name="host-server-faults"></a>Falhas de servidor de anfitrião 
Olá VM está alojado num servidor físico que está a ser executado no interior de um datacenter do Azure. Olá servidor físico executa um agente chamado Olá o agente do anfitrião na adição tooa alguns outros componentes do Azure. Quando estes componentes de software do Azure num servidor físico Olá deixar de responder, sistema de monitorização de Olá aciona um reinício de recuperação de tooattempt hello do servidor de anfitrião. Olá VM está normalmente disponível novamente dentro de cinco minutos e continua toolive no Olá mesmo anfitrião como anteriormente.

Falhas de servidor são normalmente causadas por falhas de hardware, como falha de Olá de um disco rígido ou unidade de estado sólido. Azure monitoriza estes ocorrências continuamente, identifica erros subjacente Olá e lança atualizações, depois de serem implementada e testada mitigação de Olá.

Porque algumas falhas de hardware do servidor de anfitrião podem ser a servidor toothat específico, uma situação de reinício VM repetida pode ser melhorada através da reimplementação manualmente o servidor de anfitrião de tooanother Olá VM. Esta operação pode ser acionada utilizando Olá **Reimplementar** opção na página de detalhes de Olá do Olá VM ou parando e reiniciando Olá VM na Olá portal do Azure.

### <a name="auto-recovery"></a>Recuperação automática
Se não é possível reiniciar o servidor de anfitrião Olá por qualquer motivo, Olá plataforma Azure inicia um servidor de anfitrião defeituoso do recuperação automática ação tootake Olá fora de rotação para uma investigação mais aprofundada. 

Todas as VMs nesse anfitrião são automaticamente relocalizada tooa servidor de anfitrião diferente, bom estado de funcionamento. Este processo é normalmente completo em 15 minutos. toolearn mais informações sobre o processo de recuperação automática de Olá, consulte [recuperação automática de VMs](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Manutenção não planeada
Em raras ocasiões, Olá equipa de operações do Azure, poderá precisar de tooperform manutenção atividades tooensure Olá estado de funcionamento geral de Olá plataforma Azure. Este comportamento pode afetar a disponibilidade VM e que normalmente resulta numa Olá mesma ação de recuperação automática, tal como descrito anteriormente.  

Não planeadas maintenances incluem o seguinte Olá:

- Desfragmentação de nó urgente
- Atualizações de comutador de rede urgente

### <a name="vm-crashes"></a>Falhas VM
VMs pode ser reiniciado devido a problemas na Olá própria VM. carga de trabalho Olá ou função que está em execução no Olá VM pode acionar uma verificação de erros no sistema de operativo convidado Olá. Para ajudar a determinar o motivo de Olá para falhas de Olá, ver registos do sistema e aplicação Olá para VMs do Windows e hello registos de série para VMs com Linux.

### <a name="storage-related-forced-shutdowns"></a>Relacionadas com o armazenamento encerramentos forçados
As VMs no Azure baseiam-se nos discos virtuais para armazenamento de dados que está alojado numa infraestrutura de armazenamento do Azure Olá e sistema operativo. Sempre que a disponibilidade de Olá ou conectividade entre Olá VM e discos virtuais Olá associado é afetada por mais de 120 segundos, Olá plataforma Azure executa um encerramento forçado do Olá VMs tooavoid dados danificados. Olá VMs são automaticamente ligadas novamente após o restauro de conectividade de armazenamento. 

duração de Olá de encerramento Olá pode ser o mais curta cinco minutos mas pode ser bastante maior. Olá segue-se um dos casos específicos Olá que estão associados com relacionadas com o armazenamento forçados encerramentos: 

**Limita a exceder a e/s**

VMs poderão estar temporariamente encerrar quando pedidos de e/s consistentemente limitados porque o volume de Olá de operações de e/s por segundo (IOPS) excede os limites de Olá e/s de disco Olá. (Armazenamento de disco standard está limitado too500 IOPS.) toomitigate este problema, utilize striping de disco ou configurar o espaço de armazenamento Olá dentro Olá convidado VM, dependendo da carga de trabalho Olá. Para obter mais informações, consulte [configurar as VMs do Azure para otimizar o desempenho de armazenamento](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Limites de IOPS superiores estão disponíveis através do armazenamento do Azure Premium com segurança too80, 000 IOPS. Para obter mais informações, consulte [elevado desempenho Premium Storage](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Outros incidentes
Em raras circunstâncias, um problema ampla pode afetar vários servidores num datacenter do Azure. Se este problema ocorrer, Olá equipa do Azure envia subscrições de toohello afetado notificações de e-mail. Pode verificar Olá [dashboard de estado de funcionamento de serviço de Azure](https://azure.microsoft.com/status/) e Olá portal do Azure para o estado de Olá de falhas em curso e passado dos incidentes.
