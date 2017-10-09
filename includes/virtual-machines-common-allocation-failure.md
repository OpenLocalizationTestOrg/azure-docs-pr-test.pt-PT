
Se o problema do Azure não esteja endereçado neste artigo, visite Olá [fóruns do Azure no MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/). Pode publicar o seu problema nestes fóruns ou too@AzureSupport no Twitter. Além disso, pode ficheiro um pedido de suporte do Azure ao selecionar **obter suporte** no Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="general-troubleshooting-steps"></a>Passos de resolução de problemas gerais
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Resolver problemas de falhas de alocação comuns no modelo de implementação clássica Olá
Estes passos podem ajudar a resolver várias falhas de atribuição de máquinas virtuais:

* Redimensione Olá VM tooa diferentes tamanhos da VM.<br>
    Clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > sua máquina virtual > **definições** > **tamanho**. Para obter passos detalhados, consulte [redimensionar a máquina virtual de Olá](https://msdn.microsoft.com/library/dn168976.aspx).
* Eliminar todas as VMs do serviço de nuvem Olá e voltar a criar as VMs.<br>
    Clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > sua máquina virtual > **eliminar**. Em seguida, clique em **novo** > **computação** > [imagem de máquina virtual].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Resolver problemas de falhas de alocação comuns no modelo de implementação Azure Resource Manager Olá
Estes passos podem ajudar a resolver várias falhas de atribuição de máquinas virtuais:

* Parar (desalocar) todas as VMs no Olá mesmo disponibilidade definido, em seguida, reinicie cada um deles.<br>
    toostop: clique em **grupos de recursos** > o grupo de recursos > **recursos** > o conjunto de disponibilidade > **máquinas virtuais** > sua máquina virtual >  **Parar**.
  
    Depois de parar todas as VMs, selecione Olá primeira VM e clique em **iniciar**.

## <a name="background-information"></a>Informações gerais
### <a name="how-allocation-works"></a>Como funciona a alocação
servidores de Olá nos centros de dados do Azure são divididos em partições em clusters. Normalmente, um pedido de atribuição é tentado em vários clusters, mas é possível que determinadas restrições do pedido de alocação de Olá forçar o pedido do Olá plataforma Azure tooattempt Olá em apenas um cluster. Neste artigo, vamos deverá mencionar toothis como "tooa afixado cluster". Diagrama 1 abaixo ilustra Olá maiúsculas e minúsculas de uma alocação normal, que é tentada em vários clusters. Diagrama 2 ilustra Olá maiúsculas e minúsculas de uma alocação que tenha afixado tooCluster 2, uma vez que é o local onde está alojada Olá existente conjunto CS_1 do serviço de nuvem ou de disponibilidade.
![Diagrama de atribuição](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Por que motivo ocorrem falhas de atribuição
Quando um pedido de atribuição é afixado tooa cluster, não há uma maior possibilidade de toofind libertar recursos a falhar, uma vez que o agrupamento de recursos disponíveis de Olá é mais pequeno. Além disso, se o pedido de atribuição é afixado tooa cluster mas tipo Olá do recurso pedido não é suportado nesse cluster, o pedido irá falhar mesmo se tiver de cluster Olá libertar recursos. Diagrama 3 abaixo ilustra caso olá onde uma alocação afixada falha porque Olá candidato só cluster não tem recursos gratuitos. Diagrama 4 ilustra caso olá onde uma alocação afixada falha porque o cluster de candidatos apenas Olá não suporta Olá solicitado o tamanho da VM, apesar do cluster de Olá tem recursos gratuitos.

![Falha na alocação afixado](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Detalhadas cenários de falha de alocação específico de passos no modelo de implementação clássica Olá de resolução de problemas
Seguem-se cenários comuns de alocação que provocam um toobe de pedido de alocação afixada. Iremos irá aprofundar cada cenário neste artigo.

* Redimensionar uma VM ou adicionar VMs ou o serviço de nuvem função instâncias tooan existente
* Reinício parcialmente parada (desalocadas) VMs
* Reinício totalmente parada (desalocadas) VMs
* Implementações de teste/produção (plataforma como serviço apenas)
* Grupo de afinidade (proximidade VM/serviço)
* Baseado em grupo de afinidade de rede virtual

Quando receber um erro de alocação, consulte o artigo se qualquer um dos cenários de Olá descritos aplicar tooyour erro. Utilize o erro de alocação de Olá devolvido por cenário correspondente do Olá plataforma Azure tooidentify Olá. Se o pedido está afixado, remova alguns dos Olá afixação restrições tooopen clusters toomore pedido, deste modo, aumentar a hipótese de Olá de sucesso de alocação.

Em geral, desde que o erro de Olá não indica "Olá pedida não é suportado o tamanho da VM", pode sempre voltar a tentar num momento posterior, como recursos suficientes podem ter sido libertado no Olá cluster tooaccommodate o pedido. Se o problema de Olá que esse Olá pedida não é suportado o tamanho da VM, experimente um tamanho VM diferente. Caso contrário, a única opção de Olá é Olá tooremove afixação restrição.

Dois cenários comuns de falha são grupos de tooaffinity relacionados. Olá anterior, um grupo de afinidades foi utilizado tooprovide próximos tooVMs/serviço instâncias ou foi utilizada tooenable Olá criação de uma rede virtual. Olá, com introdução das redes virtuais regionais grupos de afinidades deixam toocreate necessária uma rede virtual. Com a redução de Olá de latência de rede numa infraestrutura do Azure, grupos de afinidade do Olá recomendação toouse de proximidade VM/serviço foi alterada.

Diagrama 5 abaixo apresenta taxonomia Olá dos cenários de alocação de Olá (afixado).
![Alocação afixado taxonomia](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Erro de Olá listado em cada cenário de atribuição é um formulário curto. Consulte toohello [pesquisa de cadeia de erro](#Error string lookup) para cadeias de erro detalhadas.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Cenário de alocação: Redimensionar uma VM ou adicione o serviço em nuvem existente tooan de instâncias de VMs ou função
**Erro**

Upgrade_VMSizeNotSupported ou GeneralError

**Causa desta afixação de cluster**

A pedir tooresize uma VM ou adicionar uma VM ou um serviço de nuvem existente do função instância tooan tem toobe tentada no cluster original Olá que aloja o serviço em nuvem existente Olá. Criar um novo serviço em nuvem permite Olá plataforma Azure toofind outro cluster que tem de libertar recursos ou suporta o tamanho da VM Olá que pediu.

**Solução**

Se o erro de Olá Upgrade_VMSizeNotSupported *, experimente um tamanho VM diferente. Se utilizar um tamanho VM diferente não é uma opção, mas se toouse aceitável um outro endereço IP virtual (VIP), crie um novo serviço toohost da nuvem Olá nova VM e adicionar Olá novo nuvem serviço toohello rede virtual regional onde hello existentes as VMs estão em execução. Se o serviço em nuvem existente não utilizar uma rede virtual regional, pode ainda criar uma nova rede virtual para o novo serviço de nuvem Olá e, em seguida, ligar os [rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Ver mais informações sobre [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Se o erro de Olá GeneralError *, é provável que tipo de Olá de recursos (por exemplo, um determinado tamanho da VM) é suportado pelo cluster Olá, mas Olá cluster não tem recursos gratuitos momento Olá. Semelhante toohello acima cenário, adicione recursos de computação de Olá pretendido através da criação de um novo serviço de nuvem (tenha em atenção que o novo serviço de nuvem Olá tem toouse um VIP diferente) e utilizar uma rede virtual regional tooconnect seus serviços em nuvem.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Cenário de alocação: reinício parcialmente parada (desalocadas) VMs
**Erro**

GeneralError *

**Causa desta afixação de cluster**

Desalocação parcial significa que parada (desalocadas) uma ou mais, mas não todos, VMs num serviço em nuvem. Quando parar (desalocar) uma VM, Olá associado a recursos são lançados. Reiniciar essa VM parada (desalocada), por conseguinte, é um novo pedido de alocação. Reinício de VMs num serviço em nuvem parcialmente desalocada é equivalente tooadding VMs tooan serviço de nuvem existente. pedido de alocação de Olá tem toobe tentada no cluster original Olá que aloja o serviço em nuvem existente Olá. Criação de um serviço de nuvem diferente permite Olá plataforma Azure toofind outro cluster que possui o recurso gratuito ou suporta o tamanho da VM Olá que pediu.

**Solução**

Se é aceitável toouse um VIP diferente, elimine Olá parada (desalocadas) VMs (mas mantenha Olá associado discos) e adicione Olá VMs através de um serviço cloud diferente. Utilize uma rede virtual regional tooconnect os seus serviços em nuvem:

* Se o serviço em nuvem existente utiliza uma rede virtual regional, adicione simplesmente Olá novo toohello de serviço de nuvem mesma rede virtual.
* Se o serviço em nuvem existente não utiliza uma rede virtual regional, crie uma nova rede virtual para o novo serviço de nuvem Olá e, em seguida, [ligar a sua rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Ver mais informações sobre [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Cenário de alocação: reinício totalmente parada (desalocadas) VMs
**Erro**

GeneralError *

**Causa desta afixação de cluster**

Meios de Desalocação completo que deixaram (desalocado) todas as VMs de um serviço em nuvem. Alocação de Olá pedidos toorestart que estas VMs tem toobe tentada no cluster original Olá que aloja o serviço em nuvem Olá. Criar um novo serviço em nuvem permite Olá plataforma Azure toofind outro cluster que tem de libertar recursos ou suporta o tamanho da VM Olá que pediu.

**Solução**

Se for toouse aceitável um VIP diferente, elimine Olá original parada (desalocadas) VMs (mas mantenha Olá associado discos) e elimine Olá de serviço em nuvem correspondente (Olá associado computação recursos já foram lançados quando é parada (desalocada) Olá VMs). Crie um novo Olá de tooadd do serviço em nuvem VMs novamente.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Cenário de alocação: implementações de teste/produção (plataforma como serviço apenas)
**Erro**

New_General * ou New_VMSizeNotSupported *

**Causa desta afixação de cluster**

Olá, teste a implementação e a implementação de produção de Olá de um serviço em nuvem está alojado no Olá mesmo cluster. Quando adicionar implementação segundo Olá, será tentado pedido de atribuição correspondente Olá no mesmo cluster que aloja Olá primeira implementação de Olá.

**Solução**

Elimine a implementação primeiro Olá e o serviço em nuvem original Olá e volte a implementar o serviço de nuvem Olá. Esta ação pode chegar a primeira implementação de Olá num cluster que tem suficiente toofit de libertar recursos ambas as implementações ou num cluster que suporta tamanhos de VM de Olá que pediu.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Cenário de alocação: grupo de afinidade (proximidade VM/serviço)
**Erro**

New_General * ou New_VMSizeNotSupported *

**Causa desta afixação de cluster**

Qualquer recurso de computação tooan atribuído o grupo de afinidade está vinculada tooone cluster. Novos pedidos de recursos de computação nesse grupo de afinidade estão tentados no Olá mesmo cluster onde estão alojados recursos existentes Olá. Isto acontece se os recursos novos Olá são criados através de um novo serviço em nuvem ou através de um serviço em nuvem existente.

**Solução**

Se um grupo de afinidade não é necessário, não utilize um grupo de afinidade ou agrupar os recursos de computação em vários grupos de afinidade.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Cenário de alocação: baseado em grupo de afinidade de rede virtual
**Erro**

New_General * ou New_VMSizeNotSupported *

**Causa desta afixação de cluster**

Antes de redes virtuais regionais foram introduzidas, era necessário tooassociate uma rede virtual com um grupo de afinidade. Como resultado, os recursos de computação colocados num grupo de afinidade estão vinculados por Olá restrições mesmas, conforme descrito em Olá "cenário de alocação: grupo de afinidade (proximidade VM/serviço)" secção acima. recursos de computação Olá são cluster tooone associada.

**Solução**

Se não precisar de um grupo de afinidade, crie uma nova rede virtual regional para Olá novos recursos que está a adicionar, e, em seguida, [ligar a sua rede virtual toohello nova rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Ver mais informações sobre [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Em alternativa, pode [migrar baseado em grupo de afinidade de rede virtual tooa regional rede virtual](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e, em seguida, adicione novamente os recursos de Olá assim o desejar.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Cenários de falha de alocação específico de passos no modelo de implementação Azure Resource Manager Olá de resolução de problemas detalhada
Seguem-se cenários comuns de alocação que provocam um toobe de pedido de alocação afixada. Iremos irá aprofundar cada cenário neste artigo.

* Redimensionar uma VM ou adicionar VMs ou o serviço de nuvem função instâncias tooan existente
* Reinício parcialmente parada (desalocadas) VMs
* Reinício totalmente parada (desalocadas) VMs

Quando receber um erro de alocação, consulte o artigo se qualquer um dos cenários de Olá descritos aplicar tooyour erro. Utilize o erro de alocação de Olá devolvido por cenário correspondente do Olá plataforma Azure tooidentify Olá. Se o pedido é afixado tooan de cluster existentes, remova alguns dos Olá afixação restrições tooopen clusters toomore pedido, deste modo, aumentar a hipótese de Olá de sucesso de alocação.

Em geral, desde que o erro de Olá não indica "Olá pedida não é suportado o tamanho da VM", pode sempre voltar a tentar num momento posterior, como recursos suficientes podem ter sido libertado no Olá cluster tooaccommodate o pedido. Se o problema de Olá que esse Olá pedida não é suportado o tamanho da VM, consulte abaixo para soluções.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Cenário de alocação: Redimensionar uma VM ou adicione o conjunto de disponibilidade existente tooan VMs
**Erro**

Upgrade_VMSizeNotSupported * ou GeneralError *

**Causa desta afixação de cluster**

A pedir tooresize uma VM ou adicionar um tooan VM existente conjunto de disponibilidade tem toobe tentada no cluster original Olá que aloja o conjunto de disponibilidade existente Olá. Criar um novo conjunto de disponibilidade permite Olá plataforma Azure toofind outro cluster que tem de libertar recursos ou suporta o tamanho da VM Olá que pediu.

**Solução**

Se o erro de Olá Upgrade_VMSizeNotSupported *, experimente um tamanho VM diferente. Se utilizar um tamanho VM diferente não é uma opção, pare todas as VMs no conjunto de disponibilidade de Olá. Pode, em seguida, altere o tamanho de Olá da máquina virtual Olá que irá alocar Olá tooa o cluster de VM que suporte Olá pretendido tamanho da VM.

Se o erro de Olá GeneralError *, é provável que tipo de Olá de recursos (por exemplo, um determinado tamanho da VM) é suportado pelo cluster Olá, mas Olá cluster não tem recursos gratuitos momento Olá. Se Olá VM pode fazer parte de um conjunto de disponibilidade diferente, crie uma nova VM num conjunto de disponibilidade diferente (no Olá mesma região). Esta nova VM, em seguida, pode ser adicionado toohello mesma rede virtual.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Cenário de alocação: reinício parcialmente parada (desalocadas) VMs
**Erro**

GeneralError *

**Causa desta afixação de cluster**

Desalocação parcial significa que parada (desalocada) uma ou mais, mas não todos, VMs na disponibilidade de um conjunto. Quando parar (desalocar) uma VM, Olá associado a recursos são lançados. Reiniciar essa VM parada (desalocada), por conseguinte, é um novo pedido de alocação. Reinício de VMs de um conjunto de disponibilidade parcialmente desalocada é equivalente tooadding VMs tooan existente disponibilidade definida. pedido de alocação de Olá tem toobe tentada no cluster original Olá que aloja o conjunto de disponibilidade existente Olá.

**Solução**

Pare todas as VMs na disponibilidade de Olá definida antes de reiniciar Olá primeiro. Isto irá garantir que é executada uma nova tentativa de atribuição e que um novo cluster pode ser selecionado que tenha capacidade disponível.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Cenário de alocação: reinício totalmente parada (desalocada)
**Erro**

GeneralError *

**Causa desta afixação de cluster**

Meios de Desalocação completo que deixaram (desalocado) todas as VMs num conjunto de disponibilidade. pedido de alocação de Olá toorestart estas VMs destina-se a todos os clusters que suportam Olá tamanho pretendido.

**Solução**

Selecione um novo tooallocate de tamanho VM. Se isto não resultar, tente novamente mais tarde.

## <a name="error-string-lookup"></a>Pesquisa de cadeia de erro
**New_VMSizeNotSupported***

"Olá VM tamanho (ou combinação de tamanhos de VM) necessária para esta implementação não pode ser aprovisionada devido a restrições do pedido de toodeployment. Se for possível, tente simplificar as restrições, tais como enlaces de rede virtual, implementar serviço tooa alojado sem implementações no mesmo e tooa afinidade diferentes grupo ou sem qualquer grupo de afinidade ou experimente implementar tooa noutra região. "

**New_General***

"Falha na alocação; Não é possível toosatisfy restrições no pedido. Olá nova implementação de serviço pedida está vinculada tooan o grupo de afinidade, ou tenha como destino uma rede virtual ou há uma implementação existente neste serviço alojado. Qualquer uma destas condições restringe Olá nova implementação toospecific Azure recursos. Volte a tentar mais tarde ou tente reduzir o tamanho da VM Olá ou um número de instâncias de função. Em alternativa, se possível, remova as restrições de acima mencionados Olá ou experimente implementar noutra região de tooa."

**Upgrade_VMSizeNotSupported***

"Não é possível tooupgrade a implementação de Olá. Olá pediu o tamanho da VM XXX poderão não estar disponível em recursos de Olá implementação existente Olá de suporte. Tente novamente mais tarde, tente com um tamanho VM diferente ou menor número de instâncias de função ou crie uma implementação num serviço alojado vazio com um grupo de afinidade novo ou sem vinculação ao grupo de afinidade."

**GeneralError***

"o servidor de Olá encontrou um erro interno. Repita o pedido de Olá." Ou "Tooproduce falhou uma alocação para o serviço de Olá".

