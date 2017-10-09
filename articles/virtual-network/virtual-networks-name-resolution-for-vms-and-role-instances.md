---
title: "aaaResolution para VMs e instâncias de função"
description: "Cenários de resolução de nome para o IaaS do Azure, as soluções híbridas, entre os serviços de nuvem diferente, do Active Directory e utilizando o seu próprio servidor DNS "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Resolução de nomes para VMs e instâncias de função
Dependendo de como utilizar toohost IaaS do Azure, PaaS e soluções híbridas, poderá ser necessário tooallow Olá VMs e instâncias de função que criar toocommunicate entre si. Embora esta comunicação pode ser feita através da utilização de endereços IP, é muito mais simples nomes toouse que podem ser memorizados facilmente e não alteram. 

Quando precisam de endereços IP do tooresolve domínio nomes toointernal instâncias de função e as VMs alojadas no Azure, podem utilizar um dos dois métodos:

* [Resolução de nome fornecidos pelo Azure](#azure-provided-name-resolution)
* [Resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) (que pode reencaminhar consultas toohello servidores DNS fornecidos pelo Azure) 

tipo Olá da resolução do nome que utiliza depende de como as VMs e instâncias de função necessitam toocommunicate entre si.

**Olá tabela que se segue ilustra cenários e soluções de resolução de nome correspondente:**

| **Cenário** | **Solução** | **Sufixo** |
| --- | --- | --- |
| Resolução de nome entre instâncias de função ou VMs localizados em Olá mesma rede virtual ou serviço da nuvem |[Resolução de nome fornecidos pelo Azure](#azure-provided-name-resolution) |nome de anfitrião ou o FQDN |
| Resolução de nome entre instâncias de função ou VMs localizadas em redes virtuais diferentes |Gerida pelo cliente servidores DNS reencaminhamento consultas entre vnets para a resolução pelo Azure (proxy DNS).  Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Apenas FQDN |
| Resolução de nomes de computador e o serviço no local de instâncias de função ou VMs no Azure |Gerida pelo cliente servidores DNS (por exemplo, o controlador de domínio no local, controlador de domínio só de leitura local ou um DNS secundário sincronizada com êxito utilizando transferências de zona).  Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Apenas FQDN |
| Resolução de nomes de anfitrião do Azure a partir de computadores no local |Consultas de pesquisa direta tooa gerida pelo cliente DNS servidor proxy na vnet correspondente Olá, servidor de proxy de Olá reencaminha tooAzure de consultas para a resolução. Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Apenas FQDN |
| Inversa de DNS para IPs interno |[Resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |n/d |
| Resolução de nome entre VMs ou instâncias de função localizadas nos serviços de nuvem diferente, não numa rede virtual |Não aplicável. A conectividade entre VMs e instâncias de função nos serviços de nuvem diferente não é suportada fora de uma rede virtual. |n/d |

## <a name="azure-provided-name-resolution"></a>Resolução de nome fornecidos pelo Azure
Juntamente com a resolução de nomes DNS públicos, o Azure oferece resolução dos nomes internos para VMs e Olá de instâncias de função que residem no mesmo serviço em nuvem ou de rede virtual.  VMs/instâncias num serviço em nuvem partilham Olá DNS mesmos sufixo (para que Olá hostname autónomo é suficiente) mas nos serviços de nuvem diferente de redes virtuais clássicas ter diferentes sufixos DNS pelo Olá FQDN é tooresolve necessários nomes entre os serviços de nuvem diferente.  Nas redes virtuais no modelo de implementação do Resource Manager Olá, sufixo DNS de Olá é consistente entre a rede virtual Olá (pelo Olá FQDN não é necessário) e nomes DNS podem ser atribuídos tooboth NICs e VMs. Apesar de resolução de nome fornecidos pelo Azure necessita de qualquer configuração, não é adequada à escolha de Olá para todos os cenários de implementação, como mostrado na tabela de Olá acima.

> [!NOTE]
> No caso de Olá das funções web e de trabalho, também pode aceder a endereços IP internos Olá de instâncias de função com base no Olá função nome e a instância número utilizando Olá API de REST de gestão de serviços do Azure. Para obter mais informações, consulte [referência de API de REST de gestão de serviço](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Funcionalidades e considerações
**Funcionalidades:**

* Facilidade de utilização: é necessária nenhuma configuração na ordem toouse resolução de nome fornecidos pelo Azure.
* Olá fornecidos pelo Azure resolução serviço de nomes está altamente disponível, guardar, Olá necessário toocreate e gerir clusters dos seus servidores DNS.
* Pode ser utilizado em conjunto com a suas próprias tooresolve de servidores DNS no local e os nomes de anfitrião do Azure.
* Resolução de nomes é fornecida entre instâncias de função/VMs dentro Olá mesmo serviço em nuvem sem necessidade de um FQDN.
* Resolução de nomes é fornecida entre VMs em redes virtuais que utilizam o modelo de implementação do Resource Manager Olá, sem necessidade de Olá FQDN. Redes virtuais no modelo de implementação clássica Olá requerem Olá FQDN ao resolver os nomes de serviços de nuvem diferente. 
* Pode utilizar nomes de anfitriões que melhor descrevem as implementações, em vez de trabalhar com nomes gerado automaticamente.

**Considerações:**

* Não é possível modificar o sufixo DNS do Azure-criar de Olá.
* Não é possível registar manualmente os seus próprios registos.
* WINS e NetBIOS não são suportados. (Não é possível ver as suas VMs no Explorador do Windows.)
* Os nomes de anfitrião tem de ser compatível com o DNS (tem de utilizar apenas 0-9, a-z e '-' e não pode começar nem terminar com um '-'. Consulte a secção de 3696 RFC 2.)
* O tráfego de consulta DNS está limitado para cada VM. Isto não deve afetar a maioria das aplicações.  Se a limitação do pedido é observado, certifique-se de que a colocação em cache do lado do cliente está ativada.  Para obter mais detalhes, consulte [obter Olá maioria da resolução de nome fornecidos pelo Azure](#Getting-the-most-from-Azure-provided-name-resolution).
* Apenas as VMs nos serviços de nuvem 180 primeiro Olá estão registadas para cada rede virtual de um modelo de implementação clássica. Isto não é aplicável toovirtual redes em modelos de implementação do Resource Manager.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Introdução ao hello mais da resolução de nome fornecidos pelo Azure
**A colocação em cache do lado do cliente:**

Nem todas as consultas DNS tem toobe enviada através da rede Olá.  Colocação em cache do lado do cliente ajuda a reduzir a latência e melhorar blips toonetwork de resiliência ao resolver as consultas DNS periódicas a partir de uma cache local.  Registos DNS contêm uma Time-To-Live (TTL) que permite Olá cache toostore Olá registo desde possíveis sem afetar a actualização de registo, pelo que a colocação em cache do lado do cliente é adequada para a maioria das situações.

a predefinição de Olá cliente DNS do Windows tem uma cache DNS incorporada.  Alguns Linux distros não incluem a colocação em cache por predefinição, é recomendado que um adicionadas tooeach VM com Linux (após verificar-se de que não é uma cache local já).

Há uma série de diferentes DNS colocação em cache pacotes disponíveis, por exemplo, dnsmasq, seguem-se Olá passos tooinstall dnsmasq no distros mais comuns Olá:

* **Ubuntu (utiliza resolvconf)**:
  * Basta instale o pacote de dnsmasq Olá ("sudo apt get instalação dnsmasq").
* **SUSE (utiliza netconf)**:
  * instalar Olá dnsmasq pacote ("sudo zypper instalação dnsmasq") 
  * Ativar o serviço de dnsmasq Olá ("systemctl ativar dnsmasq.service") 
  * iniciar o serviço de dnsmasq Olá ("systemctl início dnsmasq.service") 
  * Editar "/ etc/sysconfig/rede/configuração" e altere NETCONFIG_DNS_FORWARDER = "" demasiado "dnsmasq"
  * Atualizar resolv.conf ("netconfig update") tooset Olá cache como Olá local resolução DNS
* **OpenLogic (utiliza NetworkManager)**:
  * instalar Olá dnsmasq pacote ("sudo yum instalação dnsmasq")
  * Ativar o serviço de dnsmasq Olá ("systemctl ativar dnsmasq.service")
  * iniciar o serviço de dnsmasq Olá ("systemctl início dnsmasq.service")
  * Adicionar "preceder nome-servidores domínio 127.0.0.1;" too"/etc/dhclient-eth0.conf"
  * Reiniciar cache Olá de tooset ("serviço rede restart") Olá rede serviço conforme Olá local resolução DNS

> [!NOTE]
> pacote de 'dnsmasq' Olá destina-se apenas um dos Olá muitos caches DNS disponíveis Linux.  Antes de o utilizar, verifique a respetiva adequação para as suas necessidades específicas e que não existem outro cache está instalado.
> 
> 

**Tentativas do lado do cliente:**

O DNS é principalmente um protocolo UDP.  Como Olá protocolo UDP não garante a entrega de mensagens, a lógica de repetição é processada em Olá DNS próprio protocolo.  Cada cliente DNS (sistema operativo) pode apresentem um lógica de repetição diferentes consoante a preferência de criadores de Olá:

* Sistemas operativos Windows novamente depois de 1 segundo e, em seguida, novamente após outro 2, 4 e outro 4 segundos. 
* Olá predefinido Linux configuração tentativas após 5 segundos.  É recomendado toochange este tooretry 5 vezes intervalos 1 segundo.  

toocheck Olá definições atuais numa VM com Linux, 'cat /etc/resolv.conf' e observe a linha de "Opções" Olá, por ex.:

    options timeout:1 attempts:5

ficheiro de resolv.conf Olá, normalmente, é gerado para automática e não deve ser editado.  os passos específicos Olá para adicionar a linha de Olá 'as opções' variam consoante o distro:

* **Ubuntu** (utiliza resolvconf):
  * Adicionar Olá opções linha too'/etc/resolveconf/resolv.conf.d/head' 
  * Execute 'resolvconf -u' tooupdate
* **SUSE** (utiliza netconf):
  * Adicionar 'timeout:1 tentativas: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parâmetro de '/ etc/sysconfig/rede/configuração' 
  * Execute 'netconfig actualizar' tooupdate
* **OpenLogic** (utiliza NetworkManager):
  * Adicionar too'/etc/NetworkManager/dispatcher.d/11-dhclient 'eco "opções timeout:1 tentativas: 5" ' ' 
  * Execute 'reinício do serviço de rede' tooupdate

## <a name="name-resolution-using-your-own-dns-server"></a>Resolução de nomes utilizando o seu próprio servidor DNS
Existem várias situações em que as suas necessidades de resolução de nome poderão ir para além de Olá das funcionalidades fornecidas pelo Azure, por exemplo quando utilizando domínios do Active Directory ou quando necessitar de resolução de DNS entre redes virtuais (vnets).  toocover nestes cenários, o Azure oferece Olá capacidade para toouse os seus próprios servidores DNS.  

Servidores DNS dentro de uma rede virtual podem reencaminhar as resoluções do tooAzure consultas DNS recursivas tooresolve hostnames dentro da rede virtual.  Por exemplo, um domínio Controller (controlador de domínio) em execução no Azure pode responder tooDNS consultas para os domínios e reencaminhar todos os outro tooAzure de consultas.  Isto permite que as VMs toosee seus recursos no local (através de Olá DC) e o hostnames fornecidos pelo Azure (através do reencaminhador de Olá).  As resoluções de recursiva do acesso tooAzure é fornecido através de IP virtual de Olá 168.63.129.16.

Reencaminhamento de DNS também permite a resolução de DNS inter-vnet e permite que a sua tooresolve de máquinas no local hostnames fornecidos pelo Azure.  Na ordem tooresolve hostname de uma VM, o servidor DNS de Olá VM tem de residir na Olá mesmo virtual de rede e ser tooAzure de consultas de nome de anfitrião tooforward configurado.  Como o sufixo DNS de Olá é diferente em cada vnet, pode utilizar o reencaminhamento condicional regras toosend DNS consulta toohello corrigir vnet para a resolução.  Olá imagem a seguir mostra duas vnets e uma rede no local ao executar a resolução de DNS inter-vnet através deste método.  Um reencaminhador DNS de exemplo está disponível no Olá [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) e [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![Inter-vnet DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Ao utilizar a resolução de nome fornecidos pelo Azure, um sufixo DNS interno (*. internal.cloudapp.net) é fornecido tooeach VM utilizando o DHCP.  Isto permite que a resolução de nome de anfitrião como hostname Olá são registos na zona de internal.cloudapp.net Olá.  Quando utilizar a sua própria solução de resolução de nome, Olá IDNS sufixo não é fornecido tooVMs porque-interfere com outras arquiteturas DNS (por exemplo, cenários de associados a um domínio).  Em vez disso, fornecemos um marcador não está em funcionamento (reddog.microsoft.com).  

Se for necessário, pode ser determinado sufixo DNS interno de Olá através do PowerShell ou Olá API:

* Para as redes virtuais em modelos de implementação do Resource Manager, está disponível através de Olá sufixo Olá [cartão de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx) recursos ou através de Olá [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* Modelos de implementação clássica, sufixo Olá está disponível através de Olá [obter API de implementação](https://msdn.microsoft.com/library/azure/ee460804.aspx) chamar ou através de Olá [Get-AzureVM-Debug](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

Se o reencaminhamento de consultas tooAzure não conforme as suas necessidades, terá de tooprovide sua própria solução DNS.  A solução DNS necessário:

* Fornecer a resolução de nome de anfitrião apropriado, por exemplo, através de [DDNS](virtual-networks-name-resolution-ddns.md).  Tenha em atenção que se utilizar DDNS poderá ser necessário toodisable registo eliminação de DNS como concessões DHCP do Azure são muito longos e eliminação poderá remover DNS regista prematuramente. 
* Resolução recursiva adequado resolução tooallow de nomes de domínio externo.
* Estar acessível (TCP e UDP na porta 53) a partir de clientes de Olá serve e ser capaz de tooaccess Olá internet.
* Estar protegida contra o acesso a partir de Olá internet, ameaças toomitigate colocadas por agentes externos.

> [!NOTE]
> Para melhor desempenho, ao utilizar VMs do Azure como servidores DNS, IPv6 devem ser desativados e um [IP público de nível de instância](virtual-networks-instance-level-public-ip.md) deve ser atribuído o servidor DNS tooeach VM.  Se optar por toouse do Windows Server como servidor DNS, [neste artigo](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) fornece análises de desempenho adicionais e otimizações.
> 
> 

### <a name="specifying-dns-servers"></a>Especificar os servidores DNS
Quando utilizar os seus próprios servidores DNS, o Azure fornece Olá capacidade toospecify vários servidores DNS, por rede virtual ou por rede interface (Resource Manager) / (clássica) do serviço em nuvem.  Servidores DNS especificados para uma interface de rede/serviço de nuvem obter precedência sobre as especificadas para Olá de rede virtual.

> [!NOTE]
> Propriedades de ligação de rede, tais como o servidor DNS IPs, não deve ser editada diretamente no VMs do Windows, pode obter apagadas durante o serviço heal ao adaptador de rede virtual Olá obtém substituído. 
> 
> 

Ao utilizar o modelo de implementação do Resource Manager Olá, servidores DNS podem ser especificados em Olá Portal, API/modelos ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) ou o PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Ao utilizar o modelo de implementação clássica Olá, servidores DNS para a rede virtual Olá pode ser especificada em Olá Portal ou [Olá *configuração de rede* ficheiro](https://msdn.microsoft.com/library/azure/jj157100).  Para serviços em nuvem, os servidores DNS Olá são especificados através do [Olá *a configuração do serviço* ficheiro](https://msdn.microsoft.com/library/azure/ee758710) ou do PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Se alterar as definições de DNS de Olá para uma máquina virtual/virtual de rede que já tenha sido implementado, é necessário toorestart cada VM afetado para Olá alterações tootake efeito.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Modelo de implementação do Resource Manager:

* [Criar ou atualizar uma rede virtual](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Criar ou atualizar uma placa de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [Novo-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [Novo AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Modelo de implementação clássica:

* [Esquema de configuração do serviço do Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Esquema de configuração de rede virtual](https://msdn.microsoft.com/library/azure/jj157100)
* [Configurar uma rede Virtual, utilizando um ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md) 

