


Este artigo aborda algumas perguntas comuns aos utilizadores pedir sobre máquinas virtuais do Azure criadas com o modelo de implementação clássica Olá.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Pode migrar a minha VM criada no Olá implementação clássica modelo toohello novo modelo do Resource Manager?
Sim. Para obter instruções sobre como toomigrate, consulte:

* [Migrar a partir do Gestor de recursos com o Azure PowerShell de tooAzure clássico](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migrar a partir do clássico tooAzure Resource Manager utilizando a CLI do Azure](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>O que posso executar numa VM do Azure?
Todos os subscritores podem executar software de servidor numa máquina virtual do Azure. Pode executar versões recentes do Windows Server, bem como diversas distribuições em Linux. Para detalhes de suporte, veja:

• Para VMs do Windows -- [Suporte de software de servidores da Microsoft para Máquinas Virtuais do Azure](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Para VMs do Linux -- [Linux em Distribuições Apoiadas pelo Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Para imagens de cliente do Windows, determinadas versões do Windows 7 e Windows 8.1 estão disponíveis tooMSDN subscritores de benefício do Azure e os subscritores MSDN de programação e teste pay as you go para tarefas de desenvolvimento e teste. Para obter mais detalhes, incluindo instruções e limitações, veja [Imagens do cliente Windows para subscritores MSDN](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>Por que razão os grupos de afinidades vão ser preteridos?
Os grupos de afinidade são um conceito legado para um agrupamento geográfico das implementações de serviços cloud dum cliente e contas de armazenamento no Azure. Que foram originalmente fornecido desempenho da rede VM para tooimprove em estruturas de rede do Azure antecipado Olá. São também suportavam versão inicial do Olá de redes virtuais (VNets), que foram tooa limitado pequeno conjunto de hardware numa região.

rede do Azure atual Olá numa região foi concebido para que os grupos de afinidades já não são necessários. As redes virtuais estão também num âmbito regional, pelo que um grupo de afinidades já não é necessário quando utilizar uma rede virtual. Devido a melhorias toothese, já não recomendamos que os clientes utilizam grupos de afinidade, porque pode ser limitar em alguns cenários. Utilizar grupos de afinidade de será desnecessariamente associar o hardware de toospecific VMs que limita a escolha de Olá de tamanhos de VM que estão disponível tooyou. Poderá também originar erros relacionados com toocapacity quando tenta tooadd novas VMs hardware específico Olá associadas ao grupo de afinidade de Olá com estiver prestes a capacidade.

Funcionalidades de grupo de afinidade já foram preteridas no modelo de implementação Azure Resource Manager Olá e no Olá portal do Azure. Para Olá portal clássico do Azure, podemos está a descontinuar suporte para criar grupos de afinidade e criar recursos de armazenamento que são tooan afixado grupo de afinidade. Não precisa de serviços em nuvem existente toomodify que estiver a utilizar um grupo de afinidade. No entanto, não deve utilizar os grupos de afinidade para novos serviços cloud, a menos que tal seja recomendado por um profissional de suporte do Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanto armazenamento posso utilizar com uma máquina virtual?
Cada disco de dados pode ser segurança too1 TB. Olá o número de discos de dados que pode utilizar depende Olá tamanho de Olá máquina virtual. Para obter mais detalhes, veja [Tamanhos das Virtual Machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Uma conta de armazenamento do Azure fornece armazenamento de disco do sistema operativo Olá e qualquer discos de dados. Cada disco é um ficheiro .vhd armazenado como um blob de páginas. Para detalhes de preços, veja [Detalhes de Preço do Armazenamento](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Que tipos de disco rígido virtual posso utilizar?
O Azure só suporta discos rígidos virtuais fixos em formato VHD. Se tiver um VHDX que pretende que o toouse no Azure, terá de toofirst convertê-lo utilizando o Gestor de Hyper-V ou Olá [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. Depois de o fazer, utilize [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) Olá tooupload do cmdlet (no modo de gestão do serviço) conta de armazenamento do VHD tooa no Azure, pelo que pode utilizá-lo com as máquinas virtuais.

* Para obter instruções de Linux, consulte [criar e carregar um disco rígido Virtual que contém Olá sistema operativo Linux](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Para obter instruções do Windows, consulte [criar e carregar um VHD do Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>São que estas máquinas virtuais Olá igual a máquinas virtuais Hyper-V?
Em muitos aspetos forem semelhantes demasiado VMs de Hyper-V "Geração 1", mas estiver a não exatamente Olá mesmo. Fornecem de ambos os tipos de hardware virtualizado e Olá formato VHD os discos rígidos virtuais são compatíveis. Isto significa que é possível mover entre o Hyper-V e o Azure. Três diferenças principais que, por vezes, surpreendem os utilizadores, são:

* Azure não fornece acesso de consola tooa máquina de virtual. Não há nenhum tooaccess de forma uma VM até terminar arranque.
* Na maior parte dos [tamanhos](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as VMs do Azure só têm 1 adaptador de rede virtual, o que significa que também só podem ter 1 endereço IP externo. (Olá A8 e A9 tamanhos utilizam um segundo adaptador de rede para a comunicação de aplicação entre instâncias em cenários limitados.)
* As VMs do Azure não suportam as funcionalidades de VM do Hyper-V da Geração 2. Para obter detalhes sobre estas funcionalidades, veja [Especificações de Máquina Virtual para o Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) e [Descrição Geral de Máquina Virtual da Geração 2](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Estas máquinas virtuais podem utilizar a minha infraestrutura de rede existente no local?
Para máquinas de virtuais criadas no modelo de implementação clássica Olá, pode utilizar a Azure Virtual Network tooextend infraestrutura existente. abordagem de Olá é como configurar uma sucursal. Pode aprovisionar e gerir redes privadas virtuais (VPNs) no Azure, bem como ligar de forma segura-los tooon local infraestrutura de TI. Para obter detalhes, veja [Descrição Geral da Rede Virtual do Azure](../articles/virtual-network/virtual-networks-overview.md).

Irá precisar de rede de Olá toospecify que pretende que sejam Olá máquina virtual toobelong toowhen criar máquina virtual de Olá. Não é possível associar a máquina virtual tooa rede virtual existente. No entanto, pode contornar este problema ao anular a exposição Olá disco rígido virtual (VHD) da máquina virtual existente e Olá e, em seguida, utilizá-lo toocreate uma nova máquina virtual com a configuração de rede Olá que pretende.

## <a name="how-can-i-access--my-virtual-machine"></a>Como posso aceder à minha máquina virtual?
Terá de tooestablish toolog uma ligação remota na máquina virtual de toohello utilizando a ligação de ambiente de trabalho remoto para uma VM do Windows ou um Secure Shell (SSH) para uma VM com Linux. Para obter instruções, veja:

* [Como tooLog no tooa Máquina Virtual a executar o Windows Server](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Um máximo de ligações simultâneas 2 são suportadas, a menos que o servidor de Olá está configurado como um anfitrião de sessões de serviços de ambiente de trabalho remoto.  
* [Como tooLog no tooa Máquina Virtual a executar Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Por predefinição, o SSH permite um máximo de 10 ligações simultâneas. Pode aumentar este número editando o ficheiro de configuração de Olá.

Se tiver problemas com o ambiente de trabalho remoto ou SSH, instale e utilize Olá [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema de Olá extensão toohelp garantia de reparação.

Para VMs do Windows, as opções adicionais incluem:

* No Olá portal clássico do Azure, determinar Olá VM, em seguida, clique em **repor o acesso remoto** a partir da barra de comando Olá.
* Reveja [tooa de ligações de resolução de problemas de ambiente de trabalho remoto baseado no Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Utilize a comunicação remota do Windows PowerShell tooconnect toohello VM ou criar os pontos finais adicionais para outro toohello tooconnect de recursos VM. Para obter mais informações, consulte [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se estiver familiarizado com o Hyper-V, que poderá ser procurar um tooVMConnect semelhante de ferramenta. Azure não oferece uma ferramenta semelhante, porque a máquina virtual do consola acesso tooa não é suportada.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Pode utilizar dados de toostore Olá disco temporário (Olá unidade d: para Windows ou /dev/sdb1 para Linux)?
Não deve utilizar dados de toostore Olá disco temporário (Olá unidade d: por predefinição para Windows ou /dev/sdb1 para Linux). São apenas de armazenamento temporário, pelo que correria o risco de perder dados que não poderiam ser recuperados. Isto pode ocorrer quando a máquina virtual de Olá move tooa outro anfitrião. O redimensionamento de uma máquina virtual, atualizar anfitrião hello, ou uma falha de hardware no anfitrião de Olá é algumas das razões Olá que pode mover uma máquina virtual.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Como posso alterar a letra da unidade de disco temporário Olá Olá?
Na máquina virtual do Windows, pode alterar a letra de unidade de Olá pelo ficheiro de página Olá mover e reatribuição letras de unidade, mas terá de toomake se que Olá passos por uma ordem específica. Para obter instruções, consulte [alteração Olá letra da unidade de disco temporário do Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Como atualizar o sistema de operativo convidado Olá?
Olá atualização termo geralmente significa mover tooa mais recente versão do sistema operativo, permanecendo no Olá mesmo hardware. Para VMs do Azure, Olá processo para mover tooa versão mais recente é diferente para Linux e Windows:

* Para VMs com Linux, utilize os procedimentos adequados para distribuição Olá e ferramentas de gestão do pacote de Olá.
* Para uma máquina virtual do Windows, terá de servidor de Olá toomigrate utilizar algo semelhante Olá ferramentas de migração do Windows Server. Não tente SO de convidado de Olá tooupgrade, enquanto que reside no Azure. Não é suportada devido ao risco de Olá de perda de acesso toohello máquina. Se ocorrerem problemas durante a atualização de Olá, poderia perder Olá capacidade toostart um ambiente de trabalho remoto sessão e não conseguiriam tootroubleshoot capaz de problemas de Olá.

Para obter mais informações gerais sobre as ferramentas de Olá e processos para migrar um servidor do Windows, consulte [tooWindows migrar funções e funcionalidades de servidor](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>O que é o nome de utilizador predefinido Olá e palavra-passe na máquina virtual de Olá?
imagens de Olá fornecidas pelo Azure não tem um nome de utilizador previamente configurada e a palavra-passe. Ao criar a máquina virtual utilizando uma dessas imagens, terá de tooprovide um nome de utilizador e palavra-passe, que irá utilizar toolog na máquina virtual de toohello.

Se tenha esquecido palavra-passe ou nome de utilizador Olá e instalou Olá agente da VM, pode instalar e utilizar Olá [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema de Olá toofix de extensão.

Detalhes adicionais:

* Para imagens de Linux Olá, se utilizar Olá portal clássico do Azure, 'azureuser' é fornecido como um nome de utilizador predefinido, mas pode alterar esta utilizando 'Da galeria' em vez de 'Criação rápida' como Olá forma toocreate Olá virtual máquina. Utilizar 'Da galeria' também lhe permite decidir se toouse uma palavra-passe, uma chave SSH ou ambos os toolog no. Olá conta de utilizador é um utilizador sem privilégios que tenha acesso 'sudo' toorun privilegiado comandos. conta de 'raiz' Olá está desativada.
* Para as imagens do Windows, terá de tooprovide um nome de utilizador e palavra-passe quando criar Olá VM. conta de Olá é adicionada toohello grupo de administradores.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>O Azure pode executar antivírus nas minhas máquinas virtuais?
O Azure oferece várias opções para soluções de software antivírus, mas está a funcionar tooyou toomanage-lo. Por exemplo, poderá ter uma subscrição separada para o antimalware software e, vai precisar toodecide toorun análises e instala atualizações. Pode adicionar suporte de antivírus com uma extensão de VM para o Antimalware da Microsoft, o Symantec Endpoint Protection ou o Agente de TrendMicro Deep Security quando cria uma máquina virtual do Windows ou mais tarde. Olá da Symantec e TrendMicro extensões permitem-lhe utilizar uma subscrição de avaliação gratuita de tempo limitado ou uma subscrição do enterprise existente. O Antimalware da Microsoft é gratuito. Para obter mais detalhes, veja:

* [Como tooinstall e configurar o Symantec Endpoint Protection numa VM do Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Como tooinstall e configurar a segurança avançada do tendência Micro como um serviço numa VM do Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Implementar Soluções Antimalware em Máquinas Virtuais do Azure](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Quais são as minhas opções de cópia de segurança e recuperação?
O Azure Backup está disponível como pré-visualização em determinados regiões. Para obter detalhes, veja [Fazer cópia de segurança de máquinas virtuais do Azure](../articles/backup/backup-azure-vms.md). Estão disponíveis outras soluções de parceiros certificados. toofind saída que está atualmente disponível, procure Olá Azure Marketplace.

Uma opção adicional é capacidades de instantâneo de Olá toouse do blob storage. toodo isto, terá de tooshut baixo Olá VM antes de qualquer operação que depende de um instantâneo de blob. Isto guarda dados pendente, escreve e coloca o sistema de ficheiros de Olá num estado consistente.

## <a name="how-does-azure-charge-for-my-vm"></a>Como o Azure cobra pela minha VM?
Azure cobra um preço por hora com base no tamanho da VM Olá e do sistema operativo. Para horas parciais, o Azure apenas cobra minutos Olá de utilização. Se criar Olá VM com uma imagem VM que contém determinado software previamente instalado, podem aplicar horária encargos de software adicionais. Azure cobra em separado para armazenamento para o sistema operativo e os discos de dados da VM Olá. O armazenamento em disco temporário é gratuito.

São-lhe cobrados quando Olá estado da VM está em execução ou parado, mas não lhe serem cobrados quando Olá estado da VM é parado (anular atribuído). tooput uma VM no Olá parado (desalocar) de estado, efetue um dos seguintes Olá:

* Encerre ou elimine Olá VM Olá portal clássico do Azure.
* Utilize o cmdlet Stop-AzureVM de Olá, disponível no módulo do Azure PowerShell Olá.
* Utilize uma operação de encerramento função Olá no Olá API de REST de gestão do serviço e especifique StoppedDeallocated para o elemento de PostShutdownAction Olá.

Para obter mais detalhes, veja [Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>O Azure reiniciará a minha VM para manutenção?
Por vezes, o Azure reinicia a VM como parte de atualizações de manutenção regular, planeada no Olá centros de dados do Azure.

Os eventos de manutenção não planeada podem ocorrer quando o Azure deteta um problema de hardware grave que afeta a VM. Para os eventos não planeados, o Azure automaticamente migra tooa anfitrião em bom estado de VM de Olá e reinicia Olá VM.

Qualquer autónomo VM (o significado Olá VM não faz parte de um conjunto de disponibilidade), Azure notifica o administrador de serviços da subscrição Olá por e-mail, pelo menos, uma semana antes da manutenção planeada porque Olá VMs foi necessário reiniciar durante a atualização de Olá. As aplicações em execução em VMs Olá foi tempo de inatividade.

Também pode utilizar Olá portal clássico do Azure ou os registos do Azure PowerShell tooview Olá reinício ao reinício Olá ocorreu devido tooplanned manutenção. Para obter detalhes, veja [Ver Registos de Reinício da VM](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

redundância tooprovide, coloque duas ou mais da mesma forma configurado VMs no Olá mesmo conjunto de disponibilidade. Isto ajuda a garantir que pelo menos uma VM está disponível durante a manutenção planeada ou não planeada. O Azure garante determinados níveis de disponibilidade de VM para esta configuração. Para obter mais informações, consulte [gerir a disponibilidade de Olá das máquinas virtuais](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Recursos adicionais
[Sobre as Máquinas Virtuais do Azure](../articles/virtual-machines/virtual-machines-linux-about.md)

[Criar e gerir VMs com Linux com Olá CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Criar e gerir VMs do Windows com o Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

