Azure executa periodicamente atualizações tooimprove Olá fiabilidade, o desempenho e segurança da infraestrutura de anfitrião Olá para máquinas virtuais. Estas atualizações no intervalo de componentes de software no Olá alojamento de ambiente (por exemplo, o sistema operativo, hipervisor e agentes vários implementados no anfitrião de Olá), a aplicação de patches atualizar componentes de rede, toohardware desativação. maioria de Olá destas atualizações são efetuadas sem quaisquer máquinas de virtuais do impacto toohello alojado. No entanto, há casos em que as atualizações de ter um impacto:

- Se manutenção Olá não requer um reinício, o Azure utiliza Olá toopause de migração no local VM ao anfitrião Olá é atualizada.

- Se manutenção requer um reinício, receberá um aviso de quando está a ser planeada a manutenção de Olá. Nestes casos, é-irá também ser dada uma janela de tempo em que pode iniciar manutenção Olá por si, cada vez que funciona para si.

Esta página descreve a forma como o Microsoft Azure executa ambos os tipos de manutenção. Para obter mais informações sobre eventos não planeadas (falhas), consulte o artigo sobre como gerir disponibilidade de Olá das máquinas virtuais para [Windows] (.. / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).

As aplicações em execução numa máquina virtual podem recolha informações sobre as atualizações futuras utilizando Olá Service de metadados do Azure para [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) ou [Linux] (.. / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migração de VM no local

Quando as atualizações não necessitam de um reinício total, é utilizada uma migração em direto no local. Durante a atualização de Olá Olá máquina está em pausa para cerca de 30 segundos, preservando memória Olá na RAM, enquanto o ambiente de alojamento de Olá aplica-se as atualizações necessárias do Olá e correções de erros. máquina virtual de Olá, em seguida, é retomada e relógio Olá da máquina virtual de Olá é automaticamente sincronizado.

Para VMs em conjuntos de disponibilidade, domínios de atualização são atualizado um de cada vez. Todas as VMs no domínio de uma atualização (UD) estão em pausa, atualizadas e, em seguida, retomadas antes da manutenção planeada move toohello UD seguinte.

Algumas aplicações podem ser afetadas por estes tipos de atualizações. As aplicações que executam o processamento, como o suporte de dados de transmissão em fluxo ou transcodificação ou débito elevado cenários, de rede de eventos em tempo real não podem ser concebida tootolerate uma pausa segundo 30. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Exigir um reinício de manutenção

Quando precisam de VMs toobe reiniciado para manutenção planeada, será notificado com antecedência. Manutenção planeada tem duas fases: Olá janela self-service e uma janela de manutenção agendada.

Olá **self-service janela** permite-lhe iniciar manutenção Olá nas suas VMs. Durante este tempo, pode consultar toosee cada VM o respetivo estado e verificar o resultado de Olá do último pedido manutenção.

Quando iniciar manutenção self-service, a VM é nó tooa movido que já foi atualizado e, em seguida, for ligado-lo novamente. Porque Olá VM é reiniciado, disco temporário Olá perde-se e endereços IP dinâmicos associados à interface de rede virtual foram atualizados.

Se iniciar manutenção self-service e existir um erro durante o processo de Olá, operação Olá for parada, Olá VM não é atualizada e também é removido do Olá planeada manutenção iteração. Irá ser contactado num horário posterior, com uma nova agenda e oferecido uma nova oportunidade toodo self-service manutenção. 

Depois da janela de self-service Olá, Olá **janela de manutenção agendada** começa. Durante este período de tempo, pode ainda de consulta para a janela de manutenção de Olá, mas já não será capaz de toostart manutenção de Olá por si.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerações de disponibilidade durante a manutenção planeada 

Se decidir toowait até Olá a janela de manutenção planeada, existem alguns aspetos tooconsider para manter Olá availabilty mais elevado das suas VMs. 

### <a name="paired-regions"></a>Regiões emparelhadas

Cada região do Azure se encontra emparelhado com outro região dentro Olá mesma geografia, em conjunto que efetuam um par regional. Durante a manutenção planeada, o Azure irá atualizar apenas Olá VMs numa única região de um par de região. Por exemplo, ao atualizar máquinas virtuais no Norte Central-nos de Olá, Azure irá não atualizar quaisquer máquinas virtuais no Sul Central-nos em Olá mesmo tempo. No entanto, noutras regiões como Europa do Norte pode estar em manutenção em Olá mesmo tempo, como EUA Leste. Compreender como funcionam os pares de região pode ajudar a distribuir melhor as suas VMs em regiões. Para obter mais informações, consulte [pares de região do Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Conjuntos de disponibilidade e conjuntos de dimensionamento

Quando implementar uma carga de trabalho em VMs do Azure, pode criar VMs Olá dentro de uma aplicação de tooyour elevada disponibilidade de tooprovide de conjunto de disponibilidade. Isto assegura que durante a eventos de uma interrupção ou a manutenção, pelo menos uma máquina virtual está disponível.

Dentro de um conjunto de disponibilidade, VMs individuais são distribuídas por domínios de atualização de too20 (UDs) de cópia de segurança. Durante a manutenção planeada, apenas um domínio com uma única atualização é afetado em qualquer momento. Lembre-se de que ordem Olá de domínios de atualização que está a ser afetado não necessariamente acontecer sequencialmente. 

Conjuntos de dimensionamento de máquina virtual são um recurso de computação do Azure permite-lhe toodeploy e gerir um conjunto de VMs idênticas, como um único recurso. conjunto de dimensionamento de Olá é implementado automaticamente entre domínios de atualização, como VMs num conjunto de disponibilidade. Tal como com conjuntos de disponibilidade, com conjuntos de dimensionamento de apenas um domínio com uma única atualização é afetado em qualquer momento.

Para obter mais informações sobre como configurar as máquinas virtuais de elevada disponibilidade, consulte o artigo sobre como gerir disponibilidade de Olá das suas máquinas virtuais para o Windows (.. / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).
