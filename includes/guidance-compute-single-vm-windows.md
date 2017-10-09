Este artigo descreve um conjunto de práticas comprovados para executar uma máquina virtual (VM) do Windows no Azure, prestando tooscalability de atenção, disponibilidade, capacidade de gestão e segurança.

> [!NOTE]
> O Azure tem dois modelos de implementação: [do Azure Resource Manager] [ resource-manager-overview] e clássico. Este artigo utiliza o Resource Manager, que é recomendação da Microsoft para implementações novas.
>
>

Não recomendamos utilizar uma única VM para cargas de trabalho críticas de missões, porque só é criado um único ponto de falha. Para maior disponibilidade, implemente várias VMs num [conjunto de disponibilidade][availability-set]. Para obter mais informações, veja [Running multiple VMs on Azure (Executar várias VMs no Azure)][multi-vm].

## <a name="architecture-diagram"></a>Diagrama da arquitetura

Aprovisionamento de uma VM no Azure envolve mover mais partes de Olá apenas a própria VM. Não existem elementos de computação, redes e armazenamento.

> Um documento de Visio inclui neste diagrama de arquitetura está disponível para transferência a partir do Olá [Centro de transferências da Microsoft][visio-download]. Este diagrama é no Olá "Computação - VM única" página.
>
>

![[0]][0]

* **Grupo de recursos.** Um [*grupo de recursos*][resource-manager-overview] é um contentor que retém recursos relacionados. Crie um recurso do grupo de recursos de Olá toohold para esta VM.
* **VM**. Pode aprovisionar uma VM a partir de uma lista de imagens publicadas ou a partir de um ficheiro de disco rígido virtual (VHD) que carregar tooAzure o Blob storage.
* **Disco do SO.** disco de SO de Olá é um VHD armazenado no [Storage do Azure][azure-storage]. Isto significa que o se persistir, mesmo se o computador do anfitrião de Olá fica inativo.
* **Disco temporário.** Olá é criada a VM com um disco temporário (Olá `D:` unidade no Windows). Este disco é armazenado numa unidade física no computador do anfitrião de Olá. *Não* é guardado no Armazenamento do Azure e pode ser eliminado durante os reinícios e outros eventos do ciclo de vida das VMs. Utilize este disco apenas para dados temporários, tais como ficheiros de paginação ou de troca.
* **Discos de dados.** Um [disco de dados][data-disk] é um VHD persistente utilizado para dados de aplicações. Os discos de dados são armazenados no Storage do Azure, como disco de Olá SO.
* **Rede virtual (VNet) e sub-rede.** Todas as VMs no Azure são implementadas numa VNet, a qual é dividida em sub-redes.
* **Endereço IP público.** Um endereço IP público é necessário toocommunicate com Olá VM&mdash;por exemplo, ao longo de ambiente de trabalho remoto (RDP).
* **Interface de rede (NIC).** Olá NIC permite Olá VM toocommunicate com a rede virtual Olá.
* **Grupo de Segurança de Rede (NSG).** Olá [NSG] [ nsg] tooallow/recusar utilizados sub-rede de toohello de tráfego de rede. Pode associar um NSG a uma NIC individual ou a uma sub-rede. Se associar com uma sub-rede, as regras do NSG Olá aplicam tooall VMs nessa sub-rede.
* **Diagnósticos.** Registo de diagnóstico é fundamental para gerir e resolver problemas Olá VM.

## <a name="recommendations"></a>Recomendações

Olá seguir as recomendações aplicam-se para a maioria dos cenários. Siga-as, a não ser que tenha requisitos específicos que as anulem.

### <a name="vm-recommendations"></a>Recomendações de VMs

O Azure oferece vários tamanhos de máquinas de virtuais diferentes, mas recomendamos Olá e GS-série DS porque estes tamanhos de máquina suportam [armazenamento Premium][premium-storage]. Selecione um dos seguintes tamanhos de máquina, a menos que tenha uma carga de trabalho especializada, como computação de alto desempenho. Para obter mais detalhes, veja [virtual machine sizes (tamanhos de máquinas virtuais)][virtual-machine-sizes].

Se estiver a mover um tooAzure de carga de trabalho existente, começar com o tamanho da VM Olá que é Olá mais próximo correspondência tooyour servidores no local. Em seguida, medida Olá desempenho da sua carga de trabalho real com respeitem tooCPU, memória e operações de entrada/saída de disco por segundo (IOPS) e Ajustar tamanho Olá, se necessário. Se necessitar de vários NICs para a VM, lembre-se de que o número máximo de Olá de NICs é uma função do Olá [tamanho da VM][vm-size-tables].   

Quando aprovisionar Olá VM e outros recursos, tem de especificar uma região. Geralmente, escolha uma região mais próximos utilizadores internos de tooyour ou clientes. No entanto, nem todos os tamanhos de VM poderão estar disponíveis em todas as regiões. Para obter mais informações, consulte [serviços por região][services-by-region]. uma lista de Olá tamanhos de VM disponíveis uma determinada região, execute os seguintes comandos de interface de linha de comandos do Azure (CLI) de Olá toosee:

```
azure vm sizes --location <location>
```

Para obter informações sobre como escolher uma imagem de VM publicada, consulte [navegar e selecionadas imagens da máquina virtual Windows no Azure com o Powershell ou o CLI][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Recomendações de disco e armazenamento

Para melhor desempenho de e/s de disco, recomendamos [armazenamento Premium][premium-storage], que armazena dados em unidades de estado sólido (SSDs). Custo baseia-se num presumível tamanho Olá de disco de aprovisionamento de Olá. IOPS e débito também dependem do tamanho do disco, por isso, ao aprovisionar um disco, tenha em consideração todas as três fatores (capacidade, IOPS e débito).

Crie contas de armazenamento do Azure separada para cada VM toohold Olá discos rígidos virtuais (VHDs) no tooavoid ordem atingir os limites IOPS Olá para contas de armazenamento.

Adicione um ou mais discos de dados. Quando cria um novo VHD, é não formatado. Inicie sessão no disco do Olá VM tooformat Olá. Se tiver um grande número de discos de dados, tenha em atenção de limites e/s totais Olá Olá da conta de armazenamento. Para obter mais informações, veja [Virtual machine disk limits (Limites dos discos de máquinas virtuais)][vm-disk-limits].

Sempre que possível, instale aplicações num disco de dados, o disco do SO não Olá. No entanto, algumas aplicações antigas poderão ter componentes tooinstall Olá unidade c:. Nesse caso, pode [redimensionar disco Olá SO] [ resize-os-disk] através do PowerShell.

Para melhor desempenho, crie uma conta de armazenamento separada toohold registos de diagnóstico. Para conter os registos de diagnósticos, é suficiente uma conta de armazenamento localmente redundante (LRS) standard.

### <a name="network-recommendations"></a>Recomendações de rede

endereço IP público Olá pode ser dinâmicas ou estáticas. predefinição de Olá é dinâmica.

* Reserva de um [endereço IP estático] [ static-ip] se é necessário um endereço IP fixo que não mudará &mdash; por exemplo, se precisar de toocreate um um gravar no DNS, ou precisar de Olá lista segura de tooa adicionado toobe de endereço IP.
* Também pode criar um nome de domínio completamente qualificado (FQDN) para o endereço IP Olá. Em seguida, pode registar um [registo CNAME] [ cname-record] no DNS que aponta toohello FQDN. Para obter mais informações, consulte [criar um nome de domínio completamente qualificado no portal do Azure de Olá][fqdn].

Todos os NSGs contêm um conjunto de [regras predefinidas][nsg-default-rules], incluindo uma regra que bloqueia todo o tráfego de entrada da Internet. regras de predefinidas Olá não podem ser eliminadas, mas podem substituir outras regras-los. tooenable tráfego de Internet, criar regras que permitam o tráfego de entrada toospecific portas &mdash; por exemplo, a porta 80 para HTTP.  

tooenable RDP, adicione uma regra NSG que permita o tráfego de entrada tooTCP porta 3389.

## <a name="scalability-considerations"></a>Considerações de escalabilidade

Pode dimensionar uma VM ou reduzir verticalmente ao [alterar tamanho da VM Olá](../articles/virtual-machines/windows/sizes.md). tooscale saída colocar horizontalmente, dois ou mais VMs num conjunto atrás de um balanceador de carga de disponibilidade. Para obter mais informações, consulte [executar várias VMs no Azure para escalabilidade e disponibilidade][multi-vm].

## <a name="availability-considerations"></a>Considerações de disponibilidade

Para maior disponibilidade, implemente várias VMs num conjunto de disponibilidade. Isto também fornece uma maior [contrato de nível de serviço] [ vm-sla] (SLA).

A sua VM pode ser afetada por [manutenções planeadas][planned-maintenance] ou por [manutenções não planeadas][manage-vm-availability]. Pode utilizar [registos de reinício de VM] [ reboot-logs] toodetermine se reiniciar uma VM foi causada pela manutenção planeada.

Os VHDs são armazenados no [Armazenamento do Azure][azure-storage], o qual é replicado para fins de durabilidade e disponibilidade.

tooprotect contra a perda acidental de dados durante as operações normais (por exemplo, devido a erro de utilizador), também deve implementar cópias de segurança para o ponto no tempo, utilizando [instantâneos do blob] [ blob-snapshot] ou outra ferramenta.

## <a name="manageability-considerations"></a>Considerações sobre a capacidade de gestão

**Grupos de recursos.** Colocar recursos fortemente conjugados Olá essa partilha ciclo de vida do mesma para Olá mesmo [grupo de recursos][resource-manager-overview]. Grupos de recursos permitem-lhe toodeploy e monitorizar recursos como um grupo e os custos por grupo de recursos de faturação de agregação. Também pode eliminar recursos como um conjunto, o que é muito útil para implementações de teste. Dê nomes significativos aos recursos. Que torna mais fácil toolocate um recurso específico e compreender a sua função. Veja [Recommended Naming Conventions for Azure Resources (Convenções de Nomenclatura Recomendadas para Recursos do Azure)][naming conventions].

**Diagnósticos de VMs.** Ative a monitorização e os diagnósticos, incluindo métricas básicas de estado de funcionamento, registos de infraestrutura de diagnósticos e [diagnósticos de arranque][boot-diagnostics]. Diagnóstico de arranque pode ajudar a diagnosticar uma falha de arranque, se a VM obtém-se num Estado nonbootable. Para obter mais informações, veja [Enable monitoring and diagnostics (Ativar a monitorização e os diagnósticos)][enable-monitoring]. Olá utilize [recolha de registos do Azure] [ log-collector] extensão toocollect plataforma Azure regista e carregá-los tooAzure armazenamento.   

Olá, os seguintes comandos da CLI permite o diagnóstico:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Parar uma VM.** O Azure faz uma distinção entre os estados “parada” e “desalocada”. São-lhe cobrados quando Olá estado da VM está parado, mas não quando Olá VM é desalocada.

Utilize Olá seguir CLI comando toodeallocate uma VM:

```
azure vm deallocate <resource-group> <vm-name>
```

No portal do Azure Olá, Olá **parar** botão deallocates Olá VM. No entanto, se encerrar através de Olá SO enquanto tem sessão iniciada, hello VM for parada, mas *não* anulada, pelo que, ainda será cobrada.

**Eliminar uma VM.** Se eliminar uma VM, Olá VHDs não são eliminados. Isto significa que pode eliminar em segurança Olá VM sem perda de dados. No entanto, ainda lhe será cobrado o armazenamento. Olá toodelete VHD, elimine o ficheiro de Olá de [armazenamento de BLOBs][blob-storage].

a eliminação acidental tooprevent, utilize um [bloqueio de recurso] [ resource-lock] toolock Olá recurso completo grupo ou bloqueio individuais recursos, tais como Olá VM.

## <a name="security-considerations"></a>Considerações de segurança

Utilize [Centro de segurança do Azure] [ security-center] tooget uma vista de estado de segurança de Olá dos seus recursos Azure central. Centro de segurança monitoriza potenciais problemas de segurança e fornece uma visão global do Estado de funcionamento de segurança de Olá da sua implementação. Centro de segurança está configurado por subscrição do Azure. Ativar a recolha de dados de segurança, conforme descrito em [utilize o Centro de segurança]. Quando a recolha de dados estiver ativada, o Centro de segurança analisa automaticamente quaisquer VMs criadas nessa subscrição.

**Gestão de patch.** Se estiver ativada, o Centro de segurança verifica se as atualizações críticas e de segurança estão em falta. Utilize [definições de política de grupo] [ group-policy] no Olá VM tooenable sistema automática atualizações.

**Antimalware.** Se estiver ativada, o Centro de segurança verifica se está instalado o antimalware software. Também pode utilizar o Centro de segurança tooinstall antimalware software a partir do dentro Olá portal do Azure.

**Operações.** Utilize [controlo de acesso baseado em funções] [ rbac] (RBAC) toocontrol acesso toohello Azure recursos que implementar. RBAC permite-lhe atribuir toomembers de funções de autorização da sua equipa de DevOps. Por exemplo, função de leitor de Olá pode ver os recursos do Azure, mas não criar, gerir ou eliminá-los. Algumas funções são tipos de recursos do Azure tooparticular específico. Por exemplo, função de contribuinte de Máquina Virtual de Olá pode reiniciar ou desalocar uma VM, reposição de palavra-passe de administrador de Olá, criar uma nova VM e assim sucessivamente. Outras [funções RBAC incorporadas][rbac-roles] que podem ser úteis para esta arquitetura de referência incluem [Utilizador de DevTest Labs][rbac-devtest] e [Contribuidor de Rede][rbac-network]. Um utilizador pode ser atribuído a funções de toomultiple e pode criar funções personalizadas dispõe das permissões de detalhado ainda mais.

> [!NOTE]
> RBAC não limita as ações de Olá que um utilizador com sessão iniciada para uma VM pode executar. Essas permissões são determinadas por tipo de conta Olá no convidado Olá SO.   
>
>

tooreset Olá administrador local palavra-passe, execute Olá `vm reset-access` comando da CLI do Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Utilize [registos de auditoria] [ audit-logs] toosee aprovisionamento ações e outros eventos VM.

**Encriptação de dados.** Considere [Azure Disk Encryption] [ disk-encryption] se precisar de tooencrypt Olá SO e discos de dados.

## <a name="solution-deployment"></a>Implementação de solução

Uma implementação para esta arquitetura de referência está disponível no [GitHub][github-folder]. Inclui uma VNet, um NSG e uma VM individual. toodeploy Olá arquitetura, siga estes passos:

1. Clique com o botão direito do rato em botão Olá abaixo e selecione uma "ligação aberta num novo separador" ou "Ligação aberta numa nova janela."  
   [![Implementar tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Assim que a ligação de Olá abriu no Olá portal do Azure, tem de introduzir valores para algumas das definições de Olá:

   * Olá **grupo de recursos** nome já está definido no ficheiro de parâmetros de Olá, por isso, selecione **criar novo** e introduza `ra-single-vm-rg` na caixa de texto Olá.
   * Região Olá selecione de Olá **localização** pendente caixa.
   * Não edite Olá **modelo raiz Uri** ou Olá **parâmetro raiz Uri** caixas de texto.
   * Selecione **windows** no Olá **tipo de SO** pendente caixa.
   * Analise Olá termos e condições, em seguida, clique em Olá **concordo toohello termos e condições indicadas acima** caixa de verificação.
   * Clique em Olá **Compra** botão.
3. Aguarde Olá toocomplete de implementação.
4. os ficheiros de parâmetro de Olá incluem um nome de utilizador administrador hard-coded e a palavra-passe e recomenda-se vivamente que imediatamente alterar ambas. Clique na VM com o nome de Olá `ra-single-vm0 `no Olá portal do Azure. Em seguida, clique em **Repor palavra-passe** no Olá **suporte + resolução de problemas** painel. Selecione **Repor palavra-passe** no Olá **modo** caixa de lista pendente, em seguida, selecione o novo **nome de utilizador** e **palavra-passe**. Clique em Olá **atualização** botão toopersist Olá novo nome de utilizador e palavra-passe.

Para obter informações sobre formas adicionais toodeploy esta arquitetura de referência, consulte o ficheiro Leia-me Olá Olá [orientações-único-vm][github-folder]] pasta do GitHub.

## <a name="customize-hello-deployment"></a>Personalizar a implementação de Olá
Se precisar de toochange Olá implementação toomatch às suas necessidades, siga instruções Olá Olá [Leia-me][github-folder].

## <a name="next-steps"></a>Passos seguintes
Para maior disponibilidade, implemente duas ou mais VMs por trás de um balanceador de carga. Para obter mais informações, veja [Running multiple VMs on Azure (Executar várias VMs no Azure)][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[utilize o Centro de segurança]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Arquitetura de única VM do Windows no Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
