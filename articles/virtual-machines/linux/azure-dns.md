---
title: "aaaDNS opções de resolução de nome de computadores virtuais Linux no Azure"
description: "Serviços de DNS de cenários para computadores virtuais Linux no IaaS do Azure, incluindo fornecidos de resolução de nome, o servidor DNS e traga a sua própria DNS externo no híbrida."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opções de resolução de nomes DNS para computadores virtuais Linux no Azure
O Azure oferece resolução do nome DNS por predefinição para todas as máquinas virtuais que estão numa única rede virtual. Pode implementar a sua própria solução de resolução de nome DNS ao configurar os seus próprios serviços DNS no seu máquinas virtuais que aloja do Azure. Olá seguintes cenários devem ajudar a escolher Olá que funciona para a sua situação.

* [Resolução de nome fornecidos pelo Azure](#azure-provided-name-resolution)
* [Resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server)

tipo de Olá de resolução de nomes que utiliza depende de como as máquinas virtuais e instâncias de função necessitam toocommunicate entre si.

Olá tabela que se segue ilustra cenários e soluções de resolução de nome correspondente:

| **Cenário** | **Solução** | **Sufixo** |
| --- | --- | --- |
| Nome resolução entre instâncias de função ou máquinas virtuais no Olá mesma rede virtual |[Resolução de nome fornecidos pelo Azure](#azure-provided-name-resolution) |nome de anfitrião ou nome de domínio completamente qualificado (FQDN) |
| Resolução de nome entre instâncias de função ou máquinas virtuais em redes virtuais diferentes |Gerida pelo cliente servidores DNS que reencaminham consultas entre redes virtuais para a resolução pelo Azure (proxy DNS). Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Apenas FQDN |
| Resolução de nomes de serviço de instâncias de função ou máquinas virtuais no Azure e computadores no local |Gerida pelo cliente servidores DNS (por exemplo, o controlador de domínio no local, controlador de domínio só de leitura local ou um DNS secundário sincronizada com êxito utilizando transferências de zona). Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Apenas FQDN |
| Resolução de nomes de anfitrião do Azure a partir de computadores no local |Reencaminhar consultas tooa gerida pelo cliente proxy servidor DNS na rede virtual correspondente de Olá. servidor de proxy de Olá reencaminha tooAzure de consultas para a resolução. Consulte [resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Apenas FQDN |
| Inversa de DNS para IPs interno |[Resolução de nomes utilizando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |n/d |

## <a name="name-resolution-that-azure-provides"></a>Resolução de nome fornecidos pelo Azure
Juntamente com a resolução de nomes DNS públicos, o Azure oferece resolução dos nomes internos para máquinas virtuais e Olá de instâncias de função que estão na mesma rede virtual. Em redes virtuais que são baseadas no Azure Resource Manager, o sufixo DNS Olá é consistente entre a rede virtual Olá; Olá FQDN não é necessária. Nomes DNS podem ser atribuídos tooboth placas de interface de rede (NICs) e as máquinas virtuais. Apesar de resolução de nomes de Olá fornecidos pelo Azure necessita de qualquer configuração, não é Olá adequado opção para todos os cenários de implementação, conforme visto no Olá anterior a tabela.

### <a name="features-and-considerations"></a>Funcionalidades e considerações
**Funcionalidades:**

* Nenhuma configuração é necessária toouse resolução de nome fornecidos pelo Azure.
* serviço de resolução de nome Olá fornecidos pelo Azure está altamente disponível. Não precisa de toocreate e gerir clusters dos seus servidores DNS.
* serviço de resolução de nome Olá fornecidos pelo Azure pode ser utilizado juntamente com o seus próprios tooresolve de servidores DNS no local e os nomes de anfitrião do Azure.
* Resolução de nomes é fornecida entre máquinas virtuais nas redes virtuais sem necessidade de Olá FQDN.
* Pode utilizar nomes de anfitriões que melhor descrevem as implementações em vez de trabalhar com nomes gerado automaticamente.

**Considerações:**

* Não é possível modificar o sufixo DNS Olá que o Azure cria.
* Não é possível registar manualmente os seus próprios registos.
* WINS e NetBIOS não são suportados.
* Os nomes de anfitrião tem de ser compatível com o DNS.
    Nomes têm de utilizar apenas 0-9, a-z, e '-', e não pode começar nem terminar com um '-'. Consulte RFC 3696 secção 2.
* O tráfego de consulta DNS está limitado para cada máquina virtual. Limitação não deve afetar a maioria das aplicações.  Se a limitação do pedido é observado, certifique-se de que a colocação em cache do lado do cliente está ativada.  Para obter mais informações, consulte [obter Olá maioria da resolução de nome fornecidos pelo Azure](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Introdução ao hello mais da resolução de nome fornecidos pelo Azure
**A colocação em cache do lado do cliente:**

Algumas consultas DNS não são enviadas através de rede de Olá. Colocação em cache do lado do cliente ajuda a reduzir a latência e melhorar inconsistências de toonetwork resiliência ao resolver as consultas DNS periódicas a partir de uma cache local. Registos DNS contêm uma Time-To-Live (TTL), que permite Olá cache toostore Olá registo desde possíveis sem afetar a actualização de registo. Como resultado, a colocação em cache do lado do cliente é adequada para a maioria das situações.

Algumas distribuições de Linux não incluem a colocação em cache por predefinição. Recomendamos que adicione uma máquina virtual do cache tooeach Linux depois de verificar a que não é uma cache local já.

Estão disponíveis várias DNS diferentes pacotes, tais como dnsmasq, a colocação em cache. Seguem-se Olá passos tooinstall dnsmasq no distribuições mais comuns Olá:

**Ubuntu (utiliza resolvconf)**
  * Instale Olá dnsmasq pacote ("sudo apt get instalação dnsmasq").

**SUSE (utiliza netconf)**:
1. Instale Olá dnsmasq pacote ("sudo zypper instalação dnsmasq").
2. Ative o serviço de dnsmasq Olá ("systemctl ativar dnsmasq.service").
3. Inicie o serviço de dnsmasq Olá ("systemctl início dnsmasq.service").
4. Editar "/ etc/sysconfig/rede/configuração" e alterar NETCONFIG_DNS_FORWARDER = "" demasiado "dnsmasq".
5. Atualize o resolv.conf ("netconfig update") tooset Olá cache como Olá local resolução DNS.

**CentOS pelo Software de Wave não autorizado (anteriormente OpenLogic; utiliza NetworkManager)**
1. Instale Olá dnsmasq pacote ("sudo yum instalação dnsmasq").
2. Ative o serviço de dnsmasq Olá ("systemctl ativar dnsmasq.service").
3. Inicie o serviço de dnsmasq Olá ("systemctl início dnsmasq.service").
4. Adicionar "preceder nome-servidores domínio 127.0.0.1;" too"/etc/dhclient-eth0.conf".
5. Reiniciar cache Olá de tooset ("serviço rede restart") Olá rede serviço conforme Olá local resolução DNS

> [!NOTE]
> : pacote de 'dnsmasq' Olá é apenas uma das Olá DNS muitos coloca em cache que estão disponíveis para o Linux. Antes de o utilizar, verifique a respetiva adequação para as suas necessidades e outro cache não está instalado.
>
>

**Tentativas de lado do cliente**

O DNS é principalmente um protocolo UDP. Porque Olá protocolo UDP não garante a entrega de mensagens, Olá protocolo DNS próprio processa a lógica de repetição. Cada cliente DNS (sistema operativo) pode apresentem um lógica de repetição diferentes consoante preferência do criador de Olá:

* Sistemas operativos Windows novamente depois de um segundo e, em seguida, novamente após outro duas, quatro e outro quatro segundos.
* Olá predefinido Linux configuração tentativas após cinco segundos.  Deve alterar esta tooretry cinco vezes em intervalos de um segundo.  

toocheck Olá definições atuais numa máquina virtual Linux, 'cat /etc/resolv.conf' e observe a linha de "Opções" Olá, por exemplo:

    options timeout:1 attempts:5

ficheiro de resolv.conf Olá é gerado automaticamente e não deve ser editado. Olá passos específicos que adicionar Olá 'Opções' linha variam consoante a distribuição:

**Ubuntu** (utiliza resolvconf)
1. Adicionar Olá opções linha too'/etc/resolveconf/resolv.conf.d/head'.
2. Execute tooupdate 'resolvconf -u'.

**SUSE** (utiliza netconf)
1. Adicionar 'timeout:1 tentativas: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parâmetro de '/ etc/sysconfig/rede/configuração'.
2. Execute tooupdate 'netconfig actualizar'.

**CentOS pelo Software de Wave não autorizado (anteriormente OpenLogic)** (utiliza NetworkManager)
1. Adicionar too'/etc/NetworkManager/dispatcher.d/11-dhclient 'eco "opções timeout:1 tentativas: 5" ' '.
2. Execute tooupdate 'reinício do serviço de rede'.

## <a name="name-resolution-using-your-own-dns-server"></a>Resolução de nomes utilizando o seu próprio servidor DNS
Necessidades de resolução de nome poderão ponha funcionalidades Olá fornecidos pelo Azure. Por exemplo, poderá necessitar de resolução de DNS entre redes virtuais. toocover neste cenário, pode utilizar os seus próprios servidores DNS.  

Olá, servidores DNS no pode rede virtual DNS reencaminhar consulta toorecursive resoluções de nomes de anfitrião do Azure tooresolve que estão na mesma rede virtual. Por exemplo, um servidor DNS que é executada no Azure pode responder tooDNS consultas para o seu próprio DNS ficheiros de zona e reencaminhar todos os outro tooAzure de consultas. Esta funcionalidade permite toosee de máquinas virtuais tanto as suas entradas nos seus ficheiros de zona e os nomes de anfitrião que o Azure oferece (através do reencaminhador de Olá). Resoluções de recursiva toohello acesso do Azure é fornecido através de IP virtual de Olá 168.63.129.16.

Reencaminhamento de DNS também permite a resolução de DNS entre redes virtuais e permite que os nomes de anfitrião tooresolve no local do máquinas que o Azure oferece. tooresolve nome de anfitrião de uma máquina virtual, máquina virtual do Olá DNS server têm de residir no Olá a mesma rede virtual e ser tooAzure de consultas de nome de anfitrião tooforward configurado. Porque o sufixo DNS de Olá é diferente em cada rede virtual, pode utilizar o reencaminhamento condicional regras toosend DNS consulta toohello corrigir a rede virtual para a resolução. Olá imagem seguinte mostra duas redes virtuais e uma rede no local ao executar a resolução de DNS entre redes virtuais através deste método:

![Resolução de DNS entre redes virtuais](./media/azure-dns/inter-vnet-dns.png)

Quando utilizar a resolução de nome fornecidos pelo Azure, o sufixo DNS interno do Olá é fornecido tooeach máquina através de DHCP. Quando utilizar a sua própria solução de resolução de nome, este sufixo não é fornecido toovirtual máquinas porque o sufixo de Olá interfere com outras arquiteturas DNS. toorefer toomachines pelo FQDN ou tooconfigure sufixo Olá nas suas máquinas virtuais, pode utilizar o PowerShell ou Olá sufixo de Olá toodetermine API:

* Para as redes virtuais que são geridos pelo Gestor de recursos do Azure, está disponível através de Olá sufixo Olá [cartão de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx) recursos. Também pode executar Olá `azure network public-ip show <resource group> <pip name>` comando toodisplay Olá detalhes sobre o IP público, que inclui Olá FQDN do Olá NIC.

Se o reencaminhamento de consultas tooAzure não conforme as suas necessidades, terá de tooprovide sua própria solução DNS.  A solução DNS tem de:

* Fornecer a resolução de nome de anfitrião adequado, por exemplo [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Se utilizar DDNS, poderá ser necessário a eliminação do registo DNS da toodisable. Concessões DHCP do Azure são muito longos e eliminação poderá remover registos DNS prematuramente.
* Resolução recursiva adequado resolução tooallow de nomes de domínio externo.
* Estar acessível (TCP e UDP na porta 53) a partir de clientes de Olá serve e ser capaz de tooaccess Olá Internet.
* Estar protegida contra o acesso a partir de Olá Internet toomitigate ameaças colocada por agentes externos.

> [!NOTE]
> Para melhor desempenho, quando utilizar máquinas virtuais em servidores de DNS do Azure, desative o IPv6 e atribuir um [IP público de nível de instância](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS server virtual máquina.  
>
>
