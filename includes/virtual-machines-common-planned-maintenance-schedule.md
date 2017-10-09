

## <a name="multi-and-single-instance-vms"></a>VMs de instância única e várias
Muitos clientes em execução no Azure contagem-crítico que pode agendar quando as respetivas VMs são submetidos a manutenção planeada devido a indisponibilidade de toohello – cerca de 15 minutos - que ocorre durante a manutenção. Pode utilizar o controlo de toohelp de conjuntos de disponibilidade quando VMs aprovisionadas receberem manutenção planeada.

Existem duas configurações possíveis para VMs em execução no Azure. VMs ou estão configuradas como múltiplas instâncias ou de instância única. Se as VMs estão num conjunto de disponibilidade, em seguida, estes estão configurados como várias instâncias. Tenha em atenção, mesmo único VMs podem ser implementadas num conjunto de disponibilidade, para que são tratadas como várias instâncias. Se não forem VMs num conjunto de disponibilidade, em seguida, estes estão configurados como instância única.  Para obter detalhes sobre conjuntos de disponibilidade, consulte [Olá de gerir a disponibilidade das máquinas virtuais Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Olá de gerir a disponibilidade das máquinas virtuais Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Instância toosingle de atualizações de manutenção planeada e várias instâncias VMs acontecer em separado. Reconfigurar a VMs toobe único-instância (se estiverem várias instâncias) ou toobe várias instâncias (se estiverem de instância única), pode controlar quando as respetivas VMs receberem manutenção Olá planeada. Consulte [planeada manutenção de máquinas virtuais do Linux do Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [planeada manutenção de máquinas virtuais do Azure Windows](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter detalhes sobre a manutenção planeada para VMs do Azure.

## <a name="for-multi-instance-configuration"></a>Para a configuração de várias instâncias
Pode selecionar a hora de Olá manutenção planeada afeta as VMs que são implementadas numa configuração de um conjunto de disponibilidade, removendo estas VMs de conjuntos de disponibilidade.

1. Mensagens de correio eletrónico é enviada tooyou sete dias do calendário antes Olá planeada manutenção tooyour VMs numa configuração de várias instâncias. Olá IDs de subscrição e os nomes das VMs de várias instâncias de Olá afetado são incluídos no corpo de Olá de e-mail Olá.
2. Durante a esses sete dias, pode optar por tempo Olá as instâncias são atualizadas, removendo as VMs de várias instâncias nessa região do seu conjunto de disponibilidade. Esta alteração numa causas configuração um reinício, como Olá Máquina Virtual está a mover de um anfitrião físico, direcionado para manutenção, tooanother anfitrião físico que não está direcionada para manutenção.
3. Pode remover Olá VM do respetiva conjunto de disponibilidade no Olá portal do Azure.

   1. No portal de Olá, selecione Olá VM tooremove Olá do conjunto de disponibilidade.  

   2. Em **definições**, clique em **do conjunto de disponibilidade**.

      ![Seleção de conjunto de disponibilidade](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. No Olá conjunto de disponibilidade menu pendente, selecione "Não faz parte de um conjunto de disponibilidade."

      ![Remover conjunto](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Na parte superior do Olá, clique em **guardar**. Clique em **Sim** tooacknowledge que esta ação reinicia Olá VM.

   >[!TIP]
   >Pode reconfigurar Olá toomulti-instância de VM mais tarde, selecionando um dos conjuntos de disponibilidade de Olá listado.

4. VMs removidas conjuntos de disponibilidade anfitriões de instância de tooSingle movido e não são atualizadas durante Olá planeada manutenção tooAvailability definir configurações.
5. Depois de concluída a atualização de Olá tooAvailability VMs do conjunto de (de acordo com tooschedule descrito no e-mail original Olá), deve adicionar Olá VMs com os respetivos conjuntos de disponibilidade. Tornar-se parte de um conjunto de disponibilidade reconfigura Olá VMs como várias instâncias e resulta no reinício do sistema. Normalmente, depois de concluídas todas as atualizações de várias instâncias no ambiente do Azure completo de Olá, segue manutenção de instância única.

Remover uma VM a partir de um conjunto de disponibilidade pode também ser possível utilizar o Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Para a configuração de instância única
Pode selecionar a hora de Olá manutenção planeada afeta a VMs numa configuração de instância única adicionando estas VMs em conjuntos de disponibilidade.

Passo-a-passo

1. Mensagens de correio eletrónico é enviada tooyou sete dias do calendário antes Olá planeada tooVMs de manutenção numa configuração de instância única. Olá IDs de subscrição e os nomes das VMs de instância única Olá afetado são incluídos no corpo de Olá de e-mail Olá.
2. Durante a esses sete dias, pode escolher tempo Olá sua instância reinícios, adicionando a disponibilidade de tooan VMs de instância única definida nessa mesma região. Esta alteração numa causas configuração um reinício, como Olá Máquina Virtual está a mover de um anfitrião físico, direcionado para manutenção, tooanother anfitrião físico que não está direcionada para manutenção.
3. Siga as instruções tooadd aqui existente VMs em conjuntos de disponibilidade com Olá portal do Azure e o Azure PowerShell. (Consulte exemplo de Azure PowerShell Olá que se segue estes passos.)
4. Depois destas VMs são reconfigurados como várias instâncias, são excluídos da manutenção Olá planeada tooSingle instância VMs.
5. Após a conclusão da atualização VM de instância única Olá (de acordo com tooschedule no e-mail original Olá), pode regressar Olá VMs toosingle instância removendo Olá VMs dos respetivos conjuntos de disponibilidade.

Adicionar uma VM tooan também conjunto de disponibilidade pode ser conseguida com o Azure PowerShell:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
