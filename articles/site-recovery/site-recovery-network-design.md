---
title: "aaaDesigning a infraestrutura de rede para a recuperação de desastre | Microsoft Docs"
description: "Este artigo aborda considerações de design de rede para o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Conceber a sua rede para recuperação após desastre

Este artigo é profissionais tooIT direcionados, que é responsável por arquitetar, implementar e suporte continuidade do negócio e de infraestrutura (BCDR) de recuperação de desastre, e que queiram tooleverage Microsoft Azure Site Recovery (ASR) toosupport e melhorar os serviços BCDR. Este artigo aborda considerações práticas structuring rede no site de recuperação após desastre, ser-Azure ou de outro local site. 

## <a name="overview"></a>Descrição geral
[Azure Site Recovery (ASR)](https://azure.microsoft.com/services/site-recovery/) é um serviço do Microsoft Azure que orquestra proteção Olá e recuperação das suas aplicações virtualizadas para fins de recuperação (BCDR) de desastre de continuidade de negócio. Este documento é tooguide pretendido Olá leitor através do processo de Olá da criação de redes de Olá, concentrar-se na arquitetura de intervalos de IP e sub-redes no site de recuperação de desastre Olá, quando replicar máquinas virtuais (VMs) com a recuperação de Site.

Além disso, este artigo demonstra como a recuperação de Site permite arquitetar e implementar dos serviços do Centro de dados virtual multilocal toosupport BCDR ao tempo de teste ou um desastre.

Um mundo onde espera todas as pessoas 24x7 conectividade, é mais importante do que nunca tookeep sua infraestrutura e a aplicações e funcional. objetivo Olá continuidade do negócio e recuperação após desastre (BCDR) é componentes toorestore falhou para a organização Olá rapidamente pode retomar as operações normais. Desenvolvimento toodeal de estratégias de recuperação de desastre com eventos pouco provável, devastating é muito difícil. Trata-se devido toohello dificuldade inerente de prever Olá futuro, particularmente como se relaciona com tooimprobable eventos e Olá elevada custo tooprovide adequadas medidas de proteção contra far-reaching catastrophes.

É fundamental para BCDR planeamento, o objetivo de tempo de recuperação (RTO) e o objetivo de ponto de recuperação (RPO) tem de ser definidas como parte de um plano de recuperação após desastre. Quando um desastre strikes Centro de dados do cliente Olá, utilizando o Azure Site Recovery, os clientes podem rapidamente (baixa RTO) coloque online as respetivas máquinas virtuais replicadas localizadas no Centro de dados secundária de Olá ou o Microsoft Azure com a perda de dados mínimo (RPO baixo).

Ativação pós-falha é possibilitada pela ASR que copia inicialmente designadas máquinas virtuais a partir do Centro de dados secundária de toohello de centro de dados principal de Olá ou tooAzure (dependendo do cenário de Olá) e, em seguida, atualiza periodicamente réplicas Olá. Durante o planeamento da infraestrutura, design de rede deve ser considerada como potencial constrangimento que possam impedir a partir da empresa de reunião RTO e objetivos do RPO.  

Quando os administradores estão a planear toodeploy uma solução de recuperação após desastre, é uma das questões-chave Olá no respetivos minds como Olá máquina virtual estaria acessível depois de concluída a ativação pós-falha de Olá. A ASR permite Olá administrador toochoose Olá rede toowhich uma máquina virtual seria ativação pós-falha de tooafter ligado. Se o site primário Olá é o Azure ou é um site no local gerido por um servidor VMM, em seguida, isto é conseguido utilizando o mapeamento da rede. Saiba mais sobre [mapeamento da rede no Azure tooAzure DR](site-recovery-network-mapping-azure-to-azure.md) e [mapeamento da rede a partir do VMM](site-recovery-network-mapping.md)


Ao conceber a rede de Olá para o site de recuperação Olá, o administrador de Olá tem duas opções:

* Utilize um intervalo de endereços IP diferentes para a rede de Olá no site de recuperação. Neste cenário máquina virtual de Olá após a ativação pós-falha irá obter um novo endereço IP e administrador Olá teria toodo uma atualização DNS. 
* Utilize o mesmo intervalo de endereços IP para a rede de Olá no site de recuperação Olá. Em certos cenários, os administradores preferir endereços IP de Olá tooretain têm no site primário Olá, mesmo após a ativação pós-falha de Olá. Num cenário normal, um administrador teria tooupdate Olá rotas tooindicate Olá nova localização de endereços IP Olá. Mas, no cenário de olá onde uma sub-rede de Stretch está implementada entre Olá primário e sites de recuperação de Olá, manter os endereços IP Olá para máquinas de virtuais Olá passa a ser uma boa opção. Não é possível alongar uma sub-rede de um tooan de rede no local rede do Azure ou entre duas redes do Azure.  

Quando os administradores estão a planear toodeploy uma solução de recuperação após desastre, uma das questões-chave Olá no respetiva consideração é como aplicações Olá esteja acessíveis depois de concluída a ativação pós-falha de Olá. Aplicações modernas quase sempre dependem toosome grau, de redes fisicamente a mover de um serviço de um site tooanother representa um desafio de rede. Existem duas formas principais que este problema é resolvido em soluções de recuperação após desastre. Step-by-Olá primeira abordagem é toomaintain endereços IP fixos. Apesar dos serviços de Olá mover e Olá alojar servidores em diferentes localizações físicas, aplicações demorar a configuração do endereço IP Olá com os mesmos toohello nova localização. abordagem segundo Olá envolve completamente alterar o endereço IP de Olá durante a transição de Olá para Olá o site recuperado. Cada abordagem tem vários variações de implementação que se encontram-se resumidas abaixo.

Ao conceber a rede de Olá para o site de recuperação Olá, o administrador de Olá tem duas opções:

## <a name="option-1-retain-ip-addresses"></a>Opção 1: Manter endereços IP
De uma perspetiva de processo de recuperação após desastre, utilizando endereços IP fixos aparece toobe Olá mais fácil método tooimplement, mas tem um número de potenciais desafios que, na prática, certifique-se Olá abordagem menos popular. O Azure Site Recovery fornece a capacidade de Olá endereços IP Olá tooretain em todos os cenários. Antes de decide um tooretain IP, deve receber restrições toohello que impõe nas capacidades de ativação pós-falha de Olá profundamente adequado. Observe informe-nos fatores de Olá que podem ajudá-lo toomake que um decisão tooretain endereços IP, ou não. Isto pode ser conseguido de duas formas, utilizando uma sub-rede Stretch ou efetuar uma ativação pós-falha de sub-rede completa.

### <a name="stretched-subnet"></a>Sub-rede Stretch
Aqui sub-rede Olá é disponibilizada em simultâneo no site primário e localizações de DR. Termos simples significa pode mover um servidor e o segundo site toohello da configuração de IP (Layer 3) e a rede Olá encaminhará nova localização de Olá tráfego toohello automaticamente. Este é trivial toodeal com uma perspetiva de servidor, mas tem vários desafios:

* De uma perspetiva de (camada de ligação de dados) de camada 2, serão necessários equipamento de rede que pode gerir uma VLAN Stretch, mas isto tornou-se inferior de um problema, agora é amplamente disponível. problema de Olá segundo e mais difícil é que por alongar Olá domínio de falhas potencial Olá VLAN é expandido tooboth sites, essencialmente se tornar um ponto único de falha. Embora seja uma ocorrência improvável, tiver ocorrido que um storm difusão iniciada, mas não foi possível isolado. Estamos a ter encontrado opinions mistos sobre este problema último e ter visto várias implementações com êxito, bem como "será nunca implementamos esta tecnologia aqui".
* Sub-rede Stretch não é possível se estiver a utilizar o Microsoft Azure como Olá site de DR.

### <a name="subnet-failover"></a>Ativação pós-falha de sub-rede
É vantagens Olá tooobtain de ativação pós-falha de sub-rede de tooimplement possíveis da solução de sub-rede Olá esticada descrito acima sem alongar sub-rede Olá através de vários sites. Aqui determinada sub-rede estarão presente no Site 1 ou 2 do Site, mas nunca em ambos os sites em simultâneo. Ordem toomaintain Olá espaço de endereços IP no evento Olá de uma ativação pós-falha, é possível tooprogrammatically dispor Olá router infraestrutura toomove Olá sub-redes de tooanother de um site. Um Olá de cenário de ativação pós-falha sub-redes seriam mover com Olá associados a máquinas virtuais protegidas. abordagem de toothis Olá principal desvantagem é no evento Olá de uma falha tiver toomove Olá todo sub-rede, o que poderá estar OK mas pode afetar as considerações de granularidade de ativação pós-falha Olá.

Vamos examinar como uma empresa fictícias com o nome Contoso é capaz de tooreplicate a localização de recuperação de tooa VMs ao falhar através de sub-rede Olá de todo. Primeiro veremos como Contoso é capaz de toomanage as suas sub-redes enquanto replicar VMs entre duas localizações no local e, em seguida, vamos abordar como ativação pós-falha de sub-rede funciona quando [Azure é utilizado como site de recuperação de desastre Olá](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>A ativação pós-falha do tooAzure no local 
Azure Site Recovery (ASR) permite toobe Azure utilizado como um site de recuperação após desastre para as máquinas virtuais.  

Vamos examinar um cenário onde uma empresa fictícias com o nome do Woodgrove Bank tem a infraestrutura no local que alojam as respetivas aplicações de linha de negócio e estão a alojar as aplicações móveis no Azure. Conectividade entre VMs do Banco Woodgrove nos servidores do Azure e no local é fornecida por um site para site (S2S) rede privada Virtual (VPN) ou o ExpressRoute. S2S VPN permite a rede virtual do Woodgrove Bank no Azure toobe visto como uma extensão do Woodgrove Bank no local rede. Esta comunicação é ativada por S2S VPN entre o limite do Banco Woodgrove e rede virtual do Azure. Agora Woodgrove pretende toouse ASR tooreplicate respetivas cargas de trabalho executadas região do Azure primária tooanother região do Azure. Esta opção se adeque às necessidades de Olá de Woodgrove, o qual pretende uma opção de DR económica e é capaz de toostore dados em ambientes de nuvem pública. Woodgrove tem toodeal com as aplicações e configurações que dependam hard-coded endereços IP, por conseguinte, têm de um requisito tooretain endereços IP para as aplicações após a falha através de tooanother região no Azure.

Woodgrove decidiu tooassign endereços IP a partir dos recursos tooits IP endereço intervalo (172.16.1.0/24, 172.16.2.0/24) em execução no Azure.

Para Woodgrove toobe capaz de tooreplicate tooAzure respetivas máquinas virtuais, mantendo os endereços IP Olá, uma rede Virtual do Azure tem de toobe criado. Deve ser uma extensão de rede no local de Olá, para que as aplicações possam efetuar ativações pós-falha de Olá local no site tooAzure totalmente integrada. Azure permite-lhe tooadd site a site, bem como ponto a site VPN conectividade toohello redes virtuais criadas no Azure. Quando configurar a ligação de site a site, rede do Azure permite-lhe localização no local tooroute tráfego toohello (Azure chama-lo da rede local) apenas se o intervalo de endereços IP Olá é diferente do intervalo de endereços IP local Olá, porque não do Azure suporte alongar sub-redes.  Isto significa que, se tiver um 192.168.1.0/24 sub-rede no local, não é possível adicionar uma rede local 192.168.1.0/24 Olá rede do Azure. Isto é esperado porque o Azure não sabe que existem sem VMs do Active Directory na sub-rede Olá e essa sub-rede Olá está a ser criada apenas para fins de DR. não tem em conflito toobe toocorrectly consegue encaminhar o tráfego de rede fora de uma rede Azure Olá sub-redes rede Olá e Olá da rede local.

![Antes da ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design7.png)

Antes da ativação pós-falha

toohelp Woodgrove satisfazer os seus requisitos empresariais, precisamos Olá tooimplement seguir fluxos de trabalho:

* Criar uma rede adicional, informe-nos chamá-lo a rede de recuperação, onde seria possível criar máquinas virtuais Olá efetuada a ativação pós-falha.
* tooensure que Olá IP para uma VM é mantido após uma ativação pós-falha, visite o separador de configurar toohello em propriedades VM, especificar Olá mesmo IP Olá VM tem no local e, em seguida, clique em Guardar. Quando Olá VM é efetuada a ativação pós-falha, o Azure Site Recovery atribuirá Olá IP toohello virtual máquina fornecida.

![Propriedades da rede](./media/site-recovery-network-design/network-design8.png)

Depois de ativação pós-falha de Olá é acionada e Olá máquinas de virtuais são criadas no Olá rede de recuperação com o IP de Olá assim o desejar, pode ser estabelecida rede toothis de conectividade com um [Vnet tooVnet ligação](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Se for necessário esta ação pode ser colocado em script.  Que discutimos na secção anterior Olá sobre a ativação pós-falha de sub-rede, mesmo em caso de Olá de tooAzure de ativação pós-falha, as rotas seria toobe adequadamente modificou tooreflect esse 192.168.1.0/24 foi agora movido tooAzure.

![Após a ativação pós-falha de sub-rede](./media/site-recovery-network-design/network-design9.png)

Após a ativação pós-falha

Se não tiver uma rede' Azure' conforme mostrado na imagem de Olá acima. Pode criar uma ligação de vpn do site toosite entre o 'Site primário' e a rede de recuperação após a ativação pós-falha de Olá.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Ativação pós-falha tooa secundário no local site
Informe-nos observar um cenário em que queremos manter Olá IP de cada uma das VMs Olá e concluir a ativação pós-falha Olá sub-rede em conjunto. site primário Olá tem aplicações sejam executadas na sub-rede 192.168.1.0/24. Quando ocorre a ativação pós-falha de Olá, todas as máquinas de virtuais Olá que fazem parte desta sub-rede serão efetuadas a ativação pós-falha do site de recuperação toohello e manter os seus endereços IP. Rotas terá toobe modificado adequadamente o facto de Olá tooreflect que todas as máquinas de virtuais Olá pertencente toosubnet 192.168.1.0/24 agora movido toohello site de recuperação.

Olá Olá de ilustração seguinte rotas entre terceiro site do site de recuperação do site primário e site primário e site terceiro e site de recuperação terá toobe adequadamente modificado.

Olá imagens a seguir mostra sub-redes Olá antes da ativação pós-falha de Olá. Sub-rede 192.168.0.1/24 está ativo no Olá Site primário antes da ativação pós-falha de Olá e fica ativa de Olá Site de recuperação após a ativação pós-falha de Olá

![Antes da ativação pós-falha](./media/site-recovery-network-design/network-design2.png)

Antes da ativação pós-falha

imagem de Olá abaixo mostra a redes e sub-redes após a ativação pós-falha.

![Após a ativação pós-falha](./media/site-recovery-network-design/network-design3.png)

Após a ativação pós-falha

No site secundário está no local e estiver a utilizar um toomanage de servidor do VMM em seguida, quando a ativação da proteção para uma máquina virtual específica, a ASR irá alocar recursos de rede toohello seguinte fluxo de trabalho de acordo com:

* A ASR aloca um endereço IP para cada interface de rede na máquina virtual de Olá partir Olá estático conjunto de endereços IP definido na rede de relevantes Olá para cada instância de VMM do System Center.
* Se o administrador de Olá define Olá mesmo IP conj. de endereços de rede de Olá no site de recuperação de Olá como que Olá IP do conjunto de endereços de Olá iria atribuir rede no site primário Olá, ao alocar o ASR de máquina virtual de réplica endereço toohello Olá IP Olá mesmo Endereço IP da máquina virtual primária de Olá.  IP de Olá está reservado no VMM, mas não definido como IP de ativação pós-falha no anfitrião de Hyper-v Olá. IP de ativação pós-falha num anfitrião Hyper-v está definido imediatamente antes da ativação pós-falha de Olá.


Se hello mesmo IP não estiver disponível, a ASR seria alocar algum outro endereço IP disponível do conjunto de endereços IP Olá definido.

Após Olá que VM está ativada para proteção pode utilizar o seguinte exemplo script tooverify Olá IP que foi alocada toohello máquina. Olá mesmo IP deverá ser definido como IP de ativação pós-falha e atribuído toohello VM momento Olá da ativação pós-falha:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> Cenário de Olá em máquinas virtuais utiliza DHCP, gestão de Olá de endereços IP é completamente fora do controlo de Olá de ASR. Um administrador tem tooensure Olá DHCP servir Olá endereços IP do servidor no site de recuperação Olá podem servir de Olá mesmo intervalo como do site primário Olá.
>
>



## <a name="option-2-changing-ip-addresses"></a>Opção 2: A alteração dos endereços IP
Esta abordagem parece Olá de toobe atuais mais predominantes com base no tem visto. Demora formulário Olá de alterar o endereço IP Olá cada VM que esteja envolvido na ativação pós-falha de Olá. Uma desvantagem desta abordagem requer too'learn de rede de entrada Olá ' essa aplicação Olá que estava no IPx está agora no IPy. Mesmo se IPx e IPy nomes lógicos, as entradas de DNS têm normalmente toobe alterado ou removida da cache em toda a rede de Olá e entradas em cache nas tabelas de rede tem toobe atualizado ou descarregados, por conseguinte, um período de inatividade foi ser visto consoante o modo como infraestrutura de DNS de Olá tem foi. Estes problemas, podem ser atenuados utilizando valores TTL baixos no caso de Olá das aplicações de intranet e utilizando [Manager de tráfego do Azure com o ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) para internet baseados em aplicações

### <a name="changing-hello-ip-addresses---illustration"></a>A alteração dos endereços IP de Olá - ilustração
Informe-nos observar cenário olá onde estiver a planear toouse IPs diferentes em Olá primário e sites de recuperação de Olá. No seguinte exemplo de Olá também temos um site terceiro onde as aplicações de Olá alojadas no site primário ou de recuperação podem ser acedidas.

![IP diferentes - antes da ativação pós-falha](./media/site-recovery-network-design/network-design10.png)


Imagem Olá acima, existem algumas aplicações alojadas na sub-rede 192.168.1.0/24 de sub-rede no site primário Olá, e foram configurada toocome cópias de segurança no site de recuperação de Olá na sub-rede 172.16.1.0/24 após uma ativação pós-falha. Rotas de rede/ligações VPN foram configuradas corretamente para que todos os três sites podem aceder umas às outras.

Como imagem Olá abaixo mostra, após falha através de uma ou mais aplicações, serão restaurados na sub-rede da recuperação de Olá. Neste caso, mas não é restrita toofailover Olá toda sub-rede em Olá mesmo tempo. Não são alterações tooreconfigure necessário rotas de rede ou VPN. Algumas atualizações DNS e uma ativação pós-falha irão garantir que as aplicações permanecem acessíveis. Se Olá DNS for atualizações dinâmicas tooallow configurado, em seguida, as máquinas virtuais de Olá seria registar-se utilizando Olá novas IP assim que for iniciado após uma ativação pós-falha.

![IP diferentes - após a ativação pós-falha](./media/site-recovery-network-design/network-design11.png)


Depois de falhar a ativação pós-falha Olá máquina virtual de réplica pode ter um endereço IP que não se encontra Olá mesmo como endereço IP Olá da máquina virtual primária de Olá. Máquinas virtuais irá atualizar o servidor DNS de Olá que estão a utilizar após são iniciados. As entradas de DNS têm normalmente toobe alterado ou removida da cache em toda a rede de Olá e entradas em cache nas tabelas de rede tem toobe atualizado ou descarregados, pelo que não é toobe invulgar deparam com um período de indisponibilidade enquanto estas alterações de estado de efetuar. Este problema pode ser mitigado ao:

* Utilizar baixos TTL valores para as aplicações de intranet.
* Através do Configuration Manager tráfego do Azure com o ASR para a internet, com base em aplicações.
* Utilizando Olá seguintes script dentro da sua recuperação planear tooupdate Olá servidor DNS tooensure uma atualização atempada (script Olá não é necessário se estiver configurado Olá registo DNS dinâmico)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>A alteração endereços IP Olá – DR tooAzure
Olá [configuração do funcionamento em rede de infraestrutura do Microsoft Azure como um Site de recuperação após desastre](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) blogue explica como toosetup Olá necessário a infraestrutura de rede do Azure ao reter endereços IP não é um requisito. Começa pelo descrever aplicação Olá e, em seguida, procure em como toosetup redes no local e no Azure e, em seguida, e acaba com como toodo uma ativação pós-falha de teste e uma ativação pós-falha planeada.

## <a name="next-steps"></a>Passos seguintes
[Saiba](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) como a recuperação de Site mapeia redes de origem e de destino quando um servidor do VMM está a ser site primário de Olá toomanage utilizados.
