---
title: "aaaPlan redes de Hyper-V replicação tooa site VMM secundário com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve o planeamento de rede quando replicar VMs Hyper-V tooa secundário site de VMM do System Center com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Passo 3: Planear o funcionamento em rede de VM de Hyper-V replicação tooa site secundário do VMM

Depois de rever pré-requisitos de implementação, leia esta tooplan artigo redes quando replicar máquinas virtuais Hyper-V (VMs) geridas em nuvens do System Center Virtual Machine Manager (VMM), utilizando o site secundário tooa [doAzureSiteRecovery](site-recovery-overview.md) no Olá portal do Azure. 

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Descrição geral de mapeamento de rede

Mapeamento da rede é utilizado quando replicar VMs de Hyper-V (geridos no VMM) tooa secundário datacenter. Os mapas de mapeamento de rede entre redes VM num servidor VMM de origem e redes VM no servidor VMM de destino. Mapeamento Olá seguintes:

- **Ligação de rede**— liga VMs tooappropriate redes após a ativação pós-falha. réplica de Olá VM será toohello ligado a rede de destino que está mapeado toohello rede de origem.
- **Colocação ideal**— ideal locais Olá as VMs da réplica nos servidores de anfitrião do Hyper-V. As VMs da réplica são colocadas em anfitriões que podem Olá acesso mapeadas redes VM.
- **Nenhum mapeamento da rede**— se não configurar o mapeamento da rede, as VMs de réplica será ligada tooany redes VM após a ativação pós-falha.


### <a name="example"></a>Exemplo

Eis um exemplo tooillustrate este mecanismo. Vamos organização com duas localizações em Nova Iorque e Chicago.

**Localização** | **Servidor VMM** | **Redes VM** | **Mapeado para**
---|---|---|---
Nova Iorque | O VMM NewYork| VMNetwork1 NewYork | Mapeado tooVMNetwork1-Chicago
 |  | VMNetwork2 NewYork | Não mapeados
Chicago | O VMM Chicago| VMNetwork1 Chicago | TooVMNetwork1-NewYork mapeada
 | | VMNetwork1 Chicago | Não mapeados

Neste exemplo:

- Quando é criada uma máquina virtual de réplica para qualquer máquina virtual que está ligado tooVMNetwork1-NewYork, será ligado tooVMNetwork1-Chicago.
- Quando é criada uma máquina virtual de réplica para VMNetwork2 NewYork ou VMNetwork2 Chicago, não será possível rede tooany ligado.

Eis como nuvens do VMM estão configuradas no nosso exemplo e organização Olá as redes lógicas associadas a nuvens Olá.

#### <a name="cloud-protection-settings"></a>Definições de proteção de nuvem

**Nuvem protegida** | **Proteção de nuvem** | **Rede lógica (Nova Iorque)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>
SilverCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>As definições de rede lógicas e VM

**Localização** | **Rede lógica** | **Rede VM associado**
---|---|---
Nova Iorque | LogicalNetwork1 NewYork | VMNetwork1 NewYork
Chicago | LogicalNetwork1 Chicago | VMNetwork1 Chicago
 | LogicalNetwork2Chicago | VMNetwork2 Chicago

#### <a name="target-network-settings"></a>Definições de rede de destino

Com base nestas definições, quando seleciona a rede VM de destino Olá, Olá a tabela seguinte mostra as opções de Olá que irão estar disponíveis.

**Selecionar** | **Nuvem protegida** | **Proteção de nuvem** | **Rede de destino disponível**
---|---|---|---
VMNetwork1 Chicago | SilverCloud1 | SilverCloud2 | Disponível
 | GoldCloud1 | GoldCloud2 | Disponível
VMNetwork2 Chicago | SilverCloud1 | SilverCloud2 | Não disponível
 | GoldCloud1 | GoldCloud2 | Disponível


Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem o mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá de Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.


#### <a name="failback-behavior"></a>Comportamento de reativação pós-falha

toosee o que acontece no caso de Olá de reativação pós-falha (a replicação inversa), vamos assumir que VMNetwork1 NewYork está mapeada tooVMNetwork1-Chicago com Olá seguintes definições.


**Máquina virtual** | **Rede tooVM ligado**
---|---
VM1 | Rede VMNetwork1
VM2 (réplica do VM1) | VMNetwork1 Chicago

Com estas definições, vamos rever o que acontece em alguns cenários possíveis.

**Cenário** | **Resultado**
---|---
Nenhuma alteração nas propriedades da rede Olá de VM 2 após a ativação pós-falha. | VM 1 permanece ligado toohello rede de origem.
Propriedades da rede de VM-2 foram alterados após a ativação pós-falha e está desligado. | VM-1 é desligado.
Propriedades da rede de VM-2 foram alteradas após a ativação pós-falha e está ligado tooVMNetwork2-Chicago. | Se não está mapeada VMNetwork2 Chicago, VM 1 será desligado.
Mapeamento da rede de VMNetwork1 Chicago é alterado. | VM 1 será ligado toohello rede mapeada agora tooVMNetwork1-Chicago.



## <a name="prepare-for-network-mapping"></a>Preparar o mapeamento da rede

1. Em Olá origem e destino servidores VMM, deve ter uma rede lógica associada a nuvens de origem e destino Olá. 
2. Nos servidores de origem e destino Olá, deve ter uma rede lógica do VM rede toohello ligado.
3. As VMs em anfitriões Hyper-V na localização de origem Olá devem ser ligado toohello rede VM de origem. Se estiver a utilizar apenas um único servidor do VMM, pode configurar o mapeamento entre as redes VM no Olá mesmo servidor.

Eis o que acontece quando configurar o mapeamento de rede durante a implementação da recuperação de sites:

- Quando configurar o mapeamento de rede e selecione uma rede VM de destino, Olá origem as nuvens do VMM que utilizam a rede VM de origem Olá serão apresentadas, juntamente com redes VM de destino disponíveis Olá em nuvens do destino de Olá.
- - Quando o mapeamento está configurado corretamente e a replicação está ativada, uma VM de origem serão ligadas tooits rede VM de origem e a réplica de localização de destino Olá será ligada tooits mapear a rede VM.
- Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem o mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá de Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá VM será ligado toohello primeira sub-rede Olá rede.

## <a name="connect-toovms-after-failover"></a>Ligar tooVMs após a ativação pós-falha

Ao planear a replicação e a estratégia de ativação pós-falha, uma das perguntas chave Olá é como tooconnect toohello réplica após a ativação pós-falha. Existem duas opções: 

- **Utilizar um endereço IP diferente**: pode selecionar toouse um endereço IP diferente para Olá replicado VM. Olá este cenário VM obtém um novo endereço IP, após a ativação pós-falha e é necessária uma atualização DNS.
- **Manter Olá mesmo endereço IP**: É aconselhável toouse Olá mesmo endereço IP para a réplica de Olá VM. Olá manter os mesmos endereços IP simplifica a recuperação de Olá, reduzindo relativamente a problemas de rede após a ativação pós-falha. 

## <a name="retain-ip-addresses"></a>Manter os endereços IP

Se pretender que os endereços IP de Olá tooretain de site primário Olá, após o site secundário de toohello de ativação pós-falha, pode Efetue uma ativação pós-falha de sub-rede completa e atualizar as rotas tooindicate Olá nova localização de endereços IP Olá ou alternativa implementar uma sub-rede Stretch entre Olá primário e Olá locais de recuperação.

### <a name="stretched-subnet"></a>Sub-rede Stretch

Numa sub-rede Stretch, sub-rede Olá está disponível em simultâneo em ambos os sites primários e secundários de Olá. Se mover um servidor e o site secundário do configuration toohello IP (Layer 3), rede Olá encaminhará nova localização de Olá tráfego toohello automaticamente. 

De uma perspetiva de (camada de ligação de dados) de camada 2, terá de equipamento de rede que pode gerir uma VLAN Stretch. Além disso, por alongar Olá VLAN, o domínio de falhas de potenciais Olá expande tooboth sites, essencialmente se tornar um ponto único de falha. Apesar de ser um pouco provável, pode ocorrer se um storm difusão iniciada e não pode ser isolado. 


### <a name="subnet-failover"></a>Ativação pós-falha de sub-rede

Pode executar um Olá de tooobtain de ativação pós-falha de sub-rede vantagens da sub-rede Olá stretched (ampliada), sem realmente alongá-lo. Nesta solução, uma sub-rede estará disponível no site de origem ou destino Olá, mas não em ambas em simultâneo. toomaintain Olá espaço de endereços IP no evento Olá de uma ativação pós-falha, pode dispor programaticamente Olá router infraestrutura toomove Olá sub-redes de um site tooanother. Depois de quando ocorre a ativação pós-falha, sub-redes seriam movidos com Olá associados VMs. desvantagem principal Olá é que o evento de Olá de uma falha, têm toomove Olá todo sub-rede.

### <a name="example"></a>Exemplo

Eis um exemplo de ativação pós-falha de sub-rede concluída. site primário Olá tem aplicações sejam executadas na sub-rede 192.168.1.0/24. Na ativação pós-falha, Olá todas as VMs nesta sub-rede são pós-falha toohello site secundário e manter os seus endereços IP. Rotas necessidade toobe alterar o facto de Olá tooreflect que todas as máquinas de virtuais do VM Olá pertencente toosubnet 192.168.1.0/24 agora movido toohello site secundário.

Olá gráficos seguintes mostram as sub-redes de Olá antes e após a ativação pós-falha:

- Antes da ativação pós-falha, 192.168.0.1/24 sub-rede está ativo no site de origem Olá, ficar ativo no site secundário Olá após a ativação pós-falha.
- Olá rotas entre terceiro site do site de recuperação do site primário e site primário e o terceiro local e o site de recuperação terá toobe adequadamente modificado.

**Antes da ativação pós-falha**

![Antes da ativação pós-falha](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Após a ativação pós-falha**

![Após a ativação pós-falha](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Após a ativação pós-falha, eis o que acontece:

- Recuperação de site atribui um endereço IP para cada interface de rede no Olá VM, de Olá estático conjunto de endereços IP na rede relevantes Olá, para cada instância VMM.
- Se o conjunto de endereços IP Olá no site secundário Olá Olá igual no site de origem Olá, a recuperação de sites aloca Olá mesmo IP endereço (Olá de VM de origem) toohello VM de réplica. endereço IP Olá está reservado no VMM, mas não está definida como endereço IP de ativação pós-falha de Olá no anfitrião de Hyper-V Olá. endereço IP de ativação pós-falha de Olá num anfitrião Hyper-v está definido imediatamente antes da ativação pós-falha de Olá.
- Se hello mesmo endereço IP não estiver disponível, a recuperação de sites aloca outro endereço IP disponível a partir de conjunto de Olá.
- Se as VMs utilizam DHCP, a recuperação de Site não gere os endereços IP de Olá. Terá de toocheck Olá DHCP server no site secundário Olá pode alocar o endereço do Olá mesmo intervalo como site de origem Olá.

### <a name="validate-hello-ip-address"></a>Validar o endereço IP Olá

Depois de ativar a proteção para uma VM, pode utilizar o seguinte exemplo script tooverify Olá endereço atribuído toohello VM. Olá mesmo endereço IP será definido como endereço IP de ativação pós-falha de Olá e atribuído toohello VM momento Olá da ativação pós-falha:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>A alteração dos endereços IP

Neste cenário, são alterados endereços IP de Olá de VMs com ativação pós-falha. desvantagem Olá desta solução é manutenção Olá necessária. Normalmente, DNS será atualizado depois de iniciar as VMs da réplica. As entradas de DNS poderão ter toobe alterado ou fluster em thenetwork e em entradas em cache atualizadas. Isto pode resultar num período de indisponibilidade. Período de indisponibilidade pode ser mitigado da seguinte forma:

- Utilize os valores TTL baixos para aplicações de intranet.
- Utilize Olá seguinte script num plano de recuperação do Site Recovery, tooupdate Olá DNS server tooensure uma atualização atempada. Não precisa de script de Olá se utilizar o registo de DNS dinâmico.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Exemplo 

Vamos ver um cenário no qual está a planear toouse diferentes endereços IP em Olá primário e sites de recuperação de Olá. Neste exemplo temos de endereços IP diferentes em sites primários e secundários e existe; o site de s uma terceira a partir dos quais as aplicações alojadas no site primário ou de recuperação de Olá pode ser acedido.

- Antes da ativação pós-falha, as aplicações são 192.168.1.0/24 sub-rede alojada no site primário Olá e são configurada toobe na sub-rede 172.16.1.0/24 no site secundário Olá após uma ativação pós-falha.
- Rotas de rede/ligações VPN foram configuradas corretamente para que todos os três sites podem aceder umas às outras.
- Após a ativação pós-falha, serão restauradas as aplicações na sub-rede da recuperação de Olá. Neste cenário, não há nenhum toofail necessidade através de sub-rede todo Olá e sem alterações são necessários tooreconfigure rotas de rede ou VPN. a ativação pós-falha de Olá e algumas atualizações DNS, certifique-se de que as aplicações permanecem acessíveis.
- Se o DNS é atualizações dinâmicas tooallow configurado, em seguida, VMs Olá irão registar-se utilizando Olá novo endereço IP, quando for iniciado após a ativação pós-falha.

**Antes da ativação pós-falha**

![IP diferentes - antes da ativação pós-falha](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Após a ativação pós-falha**

![IP diferentes - após a ativação pós-falha](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 4: preparar o VMM e o Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


