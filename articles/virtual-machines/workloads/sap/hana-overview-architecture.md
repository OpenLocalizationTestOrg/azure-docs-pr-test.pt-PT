---
title: "aaaOverview e arquitetura de SAP HANA no Azure (instâncias de grande) | Microsoft Docs"
description: "Descrição geral da arquitetura de como tooDeploy SAP HANA no Azure (instâncias de grande)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Descrição geral de SAP HANA (instâncias de grandes dimensões) e arquitetura no Azure

## <a name="what-is-sap-hana-on-azure-large-instances"></a>O que é o SAP HANA no Azure (instâncias de grande)?

SAP HANA no Azure (instância grande) é uma solução exclusivo tooAzure. Além disso tooproviding máquinas virtuais do Azure para fins de Olá da implementação e execução de SAP HANA, Azure oferece Olá possibilidade toorun e implementar SAP HANA nos servidores de bare-metal que estão dedicado tooyou como um cliente. Olá SAP HANA na solução do Azure (instâncias de grande) baseia-se em hardware bare-metal não partilhado/servidor de anfitrião que está atribuído tooyou como um cliente. hardware de servidor Olá está incorporado no carimbos de data / maiores que contêm/servidor de computação, rede e infraestrutura de armazenamento. Que, como uma combinação é TDI HANA certificado. oferta de serviço Olá de SAP HANA no Azure (instâncias de grande) oferece várias SKUs de servidor diferente ou tamanhos de carateres começadas unidades que tenham 72 CPUs e 768 GB de memória toounits que tenham 960 CPU e memória de 20 TB.

isolamento de cliente Olá dentro de carimbo de infraestrutura de Olá é efetuado na inquilinos, que, em detalhe é semelhante a:

- Rede: Isolamento de clientes na pilha de infraestrutura através de redes virtuais por inquilino atribuído do cliente. Um inquilino é atribuído tooa único cliente. Um cliente pode ter vários inquilinos. o isolamento de rede de inquilinos Olá proíbe a comunicação de rede entre os inquilinos no nível de carimbo de infraestrutura de Olá. Mesmo que os inquilinos pertencem toohello mesmo cliente.
- Componentes de armazenamento: isolamento através da máquinas de virtuais de armazenamento que tenham volumes de armazenamento atribuído tooit. Volumes de armazenamento podem ser atribuídos a máquina de virtual de armazenamento de tooone apenas. Uma máquina virtual de armazenamento é atribuída exclusivamente tooone único inquilino na pilha de infraestrutura de certificados de SAP HANA TDI Olá. Como resultado volumes de armazenamento atribuídos a máquina de virtual de armazenamento tooa podem ser acedidas num específico e relacionado inquilino apenas. E não é visível entre diferentes inquilinos implementado de Olá tem.
- Anfitrião ou servidor: uma unidade de anfitrião do servidor ou não é partilhada entre os clientes ou inquilinos. Um servidor ou o anfitrião implementado tooa cliente, é uma unidade de computação do bare-metal atómico atribuído tooone de inquilino único. **Não** criação de partições de hardware ou a criação de partições de forma recuperável que pode resultar numa, como um cliente, a partilha de um anfitrião ou um servidor com outro cliente. Volumes de armazenamento que estão atribuídos a máquina virtual de armazenamento de toohello do inquilino específico Olá são montado toosuch um servidor. Um inquilino pode ter um unidades de servidor toomany de SKUs diferentes atribuídas exclusivamente.
- Dentro de um SAP HANA no carimbo de infraestrutura do Azure (instância grande), muitos inquilinos diferentes são implementados e isolados contra entre si através de conceitos de inquilino Olá no nível de rede, armazenamento e computação. 


Estas unidades bare-metal server são suportado toorun SAP HANA apenas. camada de aplicação Olá SAP ou carga de trabalho meio-ware maligno está em execução em máquinas virtuais do Microsoft Azure. Olá infraestrutura carimbos de data / em execução Olá SAP HANA no Azure (instância grande) unidades são toohello ligado Azure Network backbones, por isso, que é a conectividade de latência baixa entre SAP HANA nas unidades do Azure (instância grande) e Virtual Machines do Azure fornecida.

Este documento é um dos cinco documentos, que abrangem tópico Olá de SAP HANA no Azure (grande instância). Neste documento, vamos aceda através de arquitetura básico Olá, responsabilidades, serviços fornecidos e um nível elevado através de funcionalidades da solução de Olá. Para a maioria das áreas de Olá, como o funcionamento em rede e a conectividade, hello outros quatro documentos são que abrangem os detalhes e desagregar pendentes. documentação de Olá de SAP HANA no Azure (instância grande) não abrange aspetos da instalação do SAP NetWeaver ou implementações de SAP NetWeaver em VMs do Azure. Este tópico é abrangido na documentação separada encontrada no Olá mesmo contentor de documentação. 


partes de cinco Olá deste guia abrangem Olá os seguintes tópicos:

- [Descrição geral de SAP HANA (instância grande) e arquitetura no Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infraestrutura de SAP HANA (instâncias de grandes dimensões) e a conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Como tooinstall e configurar o SAP HANA (instâncias de grande) no Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (instâncias de grande) elevada disponibilidade e recuperação após desastre no Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Resolução de problemas de SAP HANA (instâncias de grandes dimensões) e monitorização no Azure](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definições

Várias definições comuns são usadas em Olá arquitetura e o guia de implementação técnica. Olá tenha em atenção os seguintes termos de licenciamento e os respetivos significados:

- **IaaS:** infraestrutura como serviço
- **PaaS:** plataforma como serviço
- **SaaS:** Software como serviço
- **Componente SAP:** uma aplicação de SAP individuais, tal como ECC, BW, Gestor de solução ou EP. Componentes SAP podem ser baseados em tecnologias tradicionais ABAP ou Java ou uma aplicação não baseada em NetWeaver como objetos de negócio.
- **Ambiente de SAP:** um ou mais componentes do SAP logicamente agrupados tooperform uma função de negócio, como o desenvolvimento, QAS, formação, DR ou de produção.
- **SAP horizontal:** refere-se toohello ativos SAP completos no seu horizontal IT. Olá horizontal SAP inclui todos os ambientes de não produção e produção.
- **Sistema SAP:** Olá combinação de camada DBMS e a camada de aplicação de um sistema de desenvolvimento do SAP ERP, sistema de teste de SAP BW, sistema de produção do SAP CRM, etc. Implementações do Azure não suportam dividindo estas duas camadas entre no local e o Azure. Significa que um sistema SAP é implementado no local ou está implementado no Azure. No entanto, pode implementar Olá sistemas diferentes de um horizontal SAP para o Azure ou no local. Por exemplo, pode implementar Olá SAP CRM desenvolvimento e teste sistemas no Azure, durante a implementação de Olá SAP CRM produção sistema no local. Para SAP HANA no Azure (instâncias de grande), destina-se que alojar a camada da aplicação Olá SAP dos sistemas SAP em VMs do Azure e Olá instância de SAP HANA relacionada numa unidade no Olá instância grande HANA carimbo de data /.
- **Carimbo de instância grande:** uma pilha de infraestrutura de hardware que é o SAP HANA TDI certificada e dedicado instâncias de SAP HANA toorun no Azure.
- **SAP HANA no Azure (instâncias de grande):** nome oficial Olá oferta no Azure toorun HANA instâncias no SAP HANA TDI certificadas hardware que é implementada em carimbos de data / instância grande em diferentes regiões do Azure. Olá relacionados com o termo **instância grande HANA** é curto para SAP HANA no Azure (instâncias de grandes dimensões) e é amplamente utilizado neste guia de implementação técnica.
- **Em vários locais:** descreve um cenário onde as VMs são implementado tooan subscrição do Azure com o site para site, multilocal ou conectividade do ExpressRoute entre datacenter(s) do Olá no local e o Azure. Documentação do Azure em comum, estes tipos de implementações também estão descritos como cenários de vários locais. Olá razão para ligação Olá é tooextend domínios no local, Active Directory/OpenLDAP no local e no local DNS no Azure. Olá no local horizontal é expandida toohello recursos do Azure de Olá subscrições do Azure. Com esta extensão, Olá VMs pode fazer parte do domínio do Olá no local. Utilizadores de domínio do domínio do Olá no local podem aceder a servidores de Olá e podem executar serviços nessas VMs (por exemplo, o DBMS serviços). É possível resolução do nome e a comunicação entre as VMs implementadas no local e as VMs implementadas do Azure. Como é o cenário típico Olá no qual SAP a maioria dos recursos são implementados. Consulte os guias de Olá de [planeamento e design para o Gateway de VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [criar uma VNet com uma ligação Site a Site utilizando o portal do Azure de Olá](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para informações mais detalhadas.
- **O inquilino:** um cliente implementado no stamp instâncias grande HANA obtém isolado para um "inquilino". Um inquilino esteja isolado na rede de Olá, armazenamento e a camada de computação de outros inquilinos. Por isso, esse unidades de armazenamento e computação toohello atribuído diferentes inquilinos não é possível ver entre si ou comunicam entre si no Olá instância grande HANA carimbo nível. Um cliente pode optar por implementações de toohave em diferentes inquilinos. Mesmo assim, não há nenhuma comunicação entre inquilinos na Olá nível de carimbo de data / instância grande HANA.

Existem uma variedade de recursos adicionais que foram publicados no tópico Olá da implementação de carga de trabalho SAP na nuvem pública do Microsoft Azure. Recomenda-se vivamente que qualquer pessoa planeamento e a execução de uma implementação de SAP HANA no Azure está experiente e conhecimento de principais de Olá do IaaS do Azure e a implementação de Olá das cargas de trabalho do SAP no IaaS do Azure. Olá recursos seguintes fornecem mais informações e devem ser referenciados antes de continuar:


- [Utilizando soluções SAP em máquinas virtuais do Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certificação

Além das hello NetWeaver certificação, o SAP requer uma certificação especial para SAP HANA toosupport SAP HANA em determinados infraestruturas, como o IaaS do Azure.

Olá core nota SAP NetWeaver e tooa grau certificação de SAP HANA, é [1928533 de n. º de nota SAP – aplicações SAP no Azure: os tipos de produtos suportados e VM do Azure](https://launchpad.support.sap.com/#/notes/1928533).

Isto [2316233 de n. º de nota SAP - SAP HANA no Microsoft Azure (instâncias de grande)](https://launchpad.support.sap.com/#/notes/2316233/E) também é significativa. Abrange a solução de Olá descrita neste guia. Além disso, são suportado toorun SAP HANA. o tipo de GS5 VM Olá do Azure. [Informações para este cenário são publicadas no Web site do SAP Olá](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Olá SAP HANA na solução do Azure (instâncias de grande) referido tooin SAP nota #2316233 disponibiliza à Microsoft e os clientes SAP Olá capacidade toodeploy grande SAP Business Suite, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA ou outras cargas de trabalho de SAP HANA no Azure. solução Olá baseia-se no Olá SAP-HANA certificada carimbo de hardware dedicado ([SAP HANA adaptados Datacenter integração – TDI](https://scn.sap.com/docs/DOC-63140)). A ser executado como um TDI de HANA SAP solução configurada fornece-lhe com confiança de Olá de saber que todas as aplicações baseadas em SAP HANA (incluindo o SAP Business Suite no SAP HANA, SAP Business armazém (BW) em SAP HANA, S4/HANA e BW4/HANA) são acontecimentos toowork Olá infraestrutura de hardware.

Em comparação com toorunning SAP HANA em Virtual Machines do Azure esta solução tem uma vantagem — proporciona muito maiores volumes de memória. Se quiser tooenable esta solução, existem alguns aspetos fundamentais toounderstand:

- camada da aplicação Olá SAP e aplicações SAP não executam no Azure máquinas virtuais (VMs) que estão alojadas no carimbos de data / Olá habitual de hardware do Azure.
- Cliente infraestrutura no local, centros de dados, e as implementações de aplicações são plataforma de nuvem do Microsoft Azure toohello ligados através do ExpressRoute do Azure (recomendado) ou rede privada Virtual (VPN). Do Active Directory (AD) e DNS também é expandido no Azure.
- instância de base de dados SAP HANA Olá para carga de trabalho HANA é executada em SAP HANA no Azure (instâncias de grande). Olá instância grande carimbo de data / está ligado em funcionamento em rede do Azure, para que o software em execução em VMs do Azure pode interagir com a instância HANA Olá em execução em instâncias de grande HANA.
- Hardware de SAP HANA no Azure (instâncias de grande) é o hardware dedicado fornecido numa infraestrutura como serviço (IaaS) com SUSE Linux Enterprise Server ou Red Hat Enterprise Linux, pré-instaladas. Tal como com máquinas de virtuais do Azure, ainda mais as atualizações e manutenção toohello sistema é da responsabilidade do cliente.
- Instalação de HANA ou qualquer toorun necessário em unidades de instâncias HANA grande componentes adicionais SAP HANA é da responsabilidade do cliente, como todas as respetivas operações em curso e as administrações de SAP HANA no Azure.
- Além disso toohello soluções descritas aqui, pode instalar outros componentes na sua subscrição do Azure que liga tooSAP HANA no Azure (instâncias de grande).  Por exemplo, os componentes que permitem a comunicação com e/ou diretamente a base de dados de SAP HANA toohello (ir servidores, servidores de RDP SAP HANA Studio, serviços de dados SAP para cenários de BI do SAP, ou soluções de monitorização de rede).
- Como no Azure, instâncias de grande HANA oferecem suporte funcionalidade de elevada disponibilidade e recuperação após desastre.

## <a name="architecture"></a>Arquitetura

Um nível elevado, ao hello SAP HANA na solução do Azure (instâncias de grande) tem Olá SAP camada da aplicação que reside na camada de base de dados de VMs do Azure e Olá que reside no hardware TDI SAP configurado localizada no carimbo instância grandes no Olá mesma região do Azure que está ligado tooAzure IaaS.

> [!NOTE]
> Terá de camada de aplicação do toodeploy Olá SAP no Olá mesma região do Azure como camada de SAP DBMS Olá. Esta regra é bem documentada publicados informações sobre a carga de trabalho do SAP no Azure. 

Olá arquitetura geral de SAP HANA no Azure (instâncias de grande) fornece uma configuração de hardware certificado SAP TDI (não virtualizados, bare metal, o servidor de elevado desempenho para a base de dados de SAP HANA Olá) e a capacidade de Olá e a flexibilidade de tooscale do Azure recursos para Olá SAP toomeet de camada de aplicação às suas necessidades.

![Descrição geral da arquitetura de SAP HANA no Azure (instâncias de grandes)](./media/hana-overview-architecture/image1-architecture.png)

arquitetura de Olá mostrada está dividida nas três secções:

- **Direito:** uma infraestrutura no local a executar aplicações diferentes nos centros de dados com os utilizadores finais aceder a aplicações de LOB (como SAP). Idealmente, isto no local, em seguida, está ligada a infraestrutura tooAzure com o Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **System Center:** mostra Azure IaaS e, neste caso, a utilização de VMs do Azure toohost SAP ou outras aplicações que utilizam o SAP HANA como um sistema DBMS. Instâncias HANA mais pequenas que fornecem a função com memória de Olá VMs do Azure são implementadas em VMs do Azure, juntamente com a respetiva camada de aplicação. Saiba mais sobre [máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/).
<br />Redes do Azure são utilizado toogroup SAP sistemas juntamente com outras aplicações em redes virtuais do Azure (VNets). Nestas VNets ligar sistemas tooon local, bem como tooSAP HANA no Azure (instâncias de grande).
<br />Para aplicações SAP NetWeaver e bases de dados que são suportados toorun no Microsoft Azure, consulte [1928533 de n. º de nota de suporte de SAP – aplicações SAP no Azure: os tipos de produtos suportados e VM do Azure](https://launchpad.support.sap.com/#/notes/1928533). Para obter a documentação sobre como implementar soluções SAP no Azure, consulte:

  -  [Utilizando o SAP em máquinas de virtuais (VMs) do Windows](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Utilizando soluções SAP em máquinas virtuais do Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **À esquerda:** mostra Olá SAP HANA TDI certificadas hardware no Olá instância grande de Azure carimbo de data /. unidades de instância grande HANA Olá são ligado toohello as VNets do Azure da sua subscrição utilizando Olá mesma tecnologia como conectividade Olá no local no Azure.

carimbo de instância de grande de Azure Olá próprio combina Olá os seguintes componentes:

- **Computação:** servidores baseados em Intel Xeon E7-8890v3 ou Intel Xeon E7-8890v4 processadores que fornecem a capacidade de computação necessário Olá e que são certificadas do SAP HANA.
- **Rede:** A unified recursos de infraestrutura de rede de alta velocidade interconnects Olá computação, armazenamento e componentes de rede local.
- **Armazenamento:** uma infraestrutura de armazenamento que é acedida através de uma infraestrutura de rede unificada. Capacidade de armazenamento específico é fornecida consoante Olá específico SAP HANA na configuração do Azure (instâncias de grande) que está a ser implementado (mais capacidade de armazenamento está disponível um custo mensal adicionais).

Numa infraestrutura de multi-inquilino de Olá do carimbo de instância grande Olá, os clientes são implementados como inquilinos isolados. Na implementação do inquilino Olá, terá de tooname uma subscrição do Azure dentro da sua inscrição do Azure. Este Olá de toobe subscrição do Azure, Olá instâncias grande HANA vai toobe cobrado contra. Estes inquilinos têm toohello uma relação de 1:1 subscrição do Azure. Rede que aconselhado é tooaccess possíveis uma unidade de instância grande HANA implementados num inquilino na região do Azure um do outro as VNets do Azure, que pertence toodifferent subscrições do Azure. Apesar das subscrições do Azure tem toobelong toohello mesma inscrição do Azure. 

Tal como acontece com as VMs do Azure, SAP HANA no Azure (instâncias de grande) é fornecido em várias regiões do Azure. Capacidades de recuperação após desastre toooffer de ordem, pode optar tooopt no. Carimbos de instância grande diferentes dentro de uma região georreplicação afiliações são ligado tooeach outros. Por exemplo, HANA grande instância carimbos dos EUA Oeste como nos EUA Leste estão ligados através de uma ligação de rede dedicada para efeitos de Olá de replicação de DR. 

Tal como pode escolher entre diferentes tipos VM com máquinas virtuais do Azure, pode escolher entre os SKUs de HANA grande instâncias diferentes adaptados para tipos diferentes de carga de trabalho de SAP HANA. SAP aplica-se rácios de socket tooprocessor memória para diferentes cargas de trabalho com base no gerações de processadores do Intel Olá — existem quatro tipos diferentes de SKU oferecidos:

A partir de Julho de 2017, SAP HANA no Azure (instâncias de grande) está disponível em várias configurações no Olá Azure regiões dos EUA oeste e dos EUA leste, leste da Austrália, Sudeste da Austrália, Europa Ocidental e Europa do Norte:

| Solução SAP | CPU | Memória | Armazenamento | Disponibilidade |
| --- | --- | --- | --- | --- |
| Otimizado para OLAP: SAP BW, BW/4HANA<br /> ou SAP HANA para carga de trabalho OLAP genérica | SAP HANA no S72 do Azure<br /> – 2x processador Intel Xeon de®® E7 8890 v3<br /> 36 núcleos de CPU e 72 threads de CPU |  768 GB |  3 TB | Disponível |
| --- | SAP HANA no S144 do Azure<br /> – 4 x processador Intel Xeon de®® E7 8890 v3<br /> 72 núcleos de CPU e 144 threads de CPU |  1,5 TB |  6 TB | Não oferecido já |
| --- | SAP HANA no S192 do Azure<br /> – 4 x processador Intel Xeon de®® E7 8890 v4<br /> 96 núcleos de CPU e 192 threads de CPU |  2.0 TB |  8 TB | Disponível |
| --- | SAP HANA no S384 do Azure<br /> – 8 x processador Intel Xeon de®® E7 8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  4.0 TB |  16 TB | TooOrder pronto |
| Otimizado para OLTP: SAP Business Suite<br /> SAP HANA ou S/4HANA (OLTP)<br /> OLTP genérico | SAP HANA no S72m do Azure<br /> – 2x processador Intel Xeon de®® E7 8890 v3<br /> 36 núcleos de CPU e 72 threads de CPU |  1,5 TB |  6 TB | Disponível |
|---| SAP HANA no S144m do Azure<br /> – 4 x processador Intel Xeon de®® E7 8890 v3<br /> 72 núcleos de CPU e 144 threads de CPU |  3.0 TB |  12 TB | Não oferecido já |
|---| SAP HANA no S192m do Azure<br /> – 4 x processador Intel Xeon de®® E7 8890 v4<br /> 96 núcleos de CPU e 192 threads de CPU  |  4.0 TB |  16 TB | Disponível |
|---| SAP HANA no S384m do Azure<br /> – 8 x processador Intel Xeon de®® E7 8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  6.0 TB |  18 TB | TooOrder pronto |
|---| SAP HANA no S384xm do Azure<br /> – 8 x processador Intel Xeon de®® E7 8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  8.0 TB |  22 TB |  TooOrder pronto |
|---| SAP HANA no S576 do Azure<br /> – 12 x processador Intel Xeon de®® E7 8890 v4<br /> 288 núcleos de CPU e 576 threads de CPU |  12.0 TB |  28 TB | TooOrder pronto |
|---| SAP HANA no S768 do Azure<br /> – 16 x processador Intel Xeon de®® E7 8890 v4<br /> 384 núcleos de CPU e 768 threads de CPU |  16.0 TB |  36 TB | TooOrder pronto |
|---| SAP HANA no S960 do Azure<br /> – 20 x processador Intel Xeon de®® E7 8890 v4<br /> 480 núcleos de CPU e 960 threads de CPU |  20.0 TB |  46 TB | TooOrder pronto |

- Núcleos de CPU = soma de núcleos de CPU não-com hyper-threading da soma de Olá de processadores de Olá de unidade do servidor de Olá.
- Threads de CPU = soma de threads de computação fornecidos pelo núcleos de CPU com hyper-threading da soma de Olá de processadores de Olá de unidade do servidor de Olá. Todas as unidades estão configuradas por toouse predefinida, o Hyper-Threading.


Olá diferentes configurações acima que se encontram disponíveis ou 'não poderão utilizar deixam de ser' referenciadas na [2316233 de n. º de nota de suporte de SAP – SAP HANA no Microsoft Azure (instâncias de grande)](https://launchpad.support.sap.com/#/notes/2316233/E). configurações de Olá, que estão marcadas como 'Pronto tooOrder' irão encontrar os respetivos entrada na Olá a nota em breve. No entanto, os SKUs de instância pode ser ordenadas já para Olá seis diferentes regiões do Azure Olá serviço da instância de grande HANA está disponível.

configurações específicas Olá escolhidas são dependentes de carga de trabalho, recursos de CPU e memória pretendida. É possível Olá de tooleverage de carga de trabalho OLTP SKUs que estão otimizados para a carga de trabalho do OLAP. 

hardware Olá base para todas as ofertas de Olá são SAP HANA TDI certificados. No entanto, iremos distinguir entre duas classes diferentes de hardware, o qual divide Olá SKUs para:

- S72, S72m, S144, S144m, S192 e S192m, que iremos Consulte tooas Olá 'Type posso de classe' de SKUs.
- S384, S384m, S384xm, S576, S768 e S960, que iremos Consulte tooas Olá 'Class II de tipo' de SKUs.

É importante toonote um carimbo de instância grande HANA concluído exclusivamente não atribuída a um único cliente &#39; utilize s. Este facto aplica-se toohello bastidores dos recursos de computação e armazenamento ligados através de uma infraestrutura de rede implementada no Azure, bem como. Infraestrutura de instâncias de grande HANA, como o Azure, implementa o cliente diferentes &quot;inquilinos&quot; que são isoladas entre si no Olá seguintes três níveis:

- Rede: Isolamento através de redes virtuais no Olá instância grande HANA carimbo de data /.
- Armazenamento: Isolamento através da máquinas de virtuais de armazenamento que tenham volumes de armazenamento atribuída e isolar os volumes de armazenamento entre inquilinos.
- Computação: Atribuição dedicada de inquilino único do servidor unidades tooa. Não difícil ou configuração soft-criação de partições de unidades do servidor. Nenhuma partilha de uma única unidade de anfitrião do servidor ou entre inquilinos. 

Como tal, as implementações de Olá de unidades de instâncias de grande HANA entre diferentes inquilinos não são visível tooeach outro. Nem HANA grande instância unidades implementada em diferentes inquilinos podem comunicar diretamente entre si no nível de carimbo de data / Olá instância grande HANA. Apenas HANA grande instância unidades dentro de um inquilino podem comunicar tooeach no Olá nível de carimbo de data / instância grande HANA.
Um inquilino implementado na Olá instância grande carimbo de data / é atribuído a faturação tooone aconselhado subscrição do Azure. No entanto, rede pode ser acedido a partir as VNets do Azure de outras subscrições do Azure dentro aconselhado Olá mesma inscrição do Azure. Se implementar com outra subscrição do Azure no Olá mesma região do Azure, também pode escolher tooask para um inquilino de instância grande HANA separado.

Existem diferenças significativas que executem SAP HANA instâncias grande HANA e SAP HANA em execução em VMs do Azure implementado no Azure:

- Não há nenhuma camada de virtualização para SAP HANA no Azure (instâncias de grande). Obter o desempenho de Olá de hardware do Olá subjacente bare-metal.
- Ao contrário do Azure, Olá SAP HANA no servidor do Azure (instâncias de grande) é tooa dedicado de cliente específico. Não há nenhum possibilidade de um anfitrião ou a unidade do servidor é difícil ou particionada de forma recuperável. Como resultado, uma unidade de instância grande HANA é utilizada como atribuída como um inquilino tooa todo e com que tooyou como um cliente. Um reinício ou encerramento do servidor de Olá não pode automaticamente toohello sistema e a implementar noutro servidor do SAP HANA. (Para o tipo de classe posso SKUs, Step-by-Olá única exceção é se o servidor poderá encontrar problemas e reimplementação toobe efetuada noutro servidor.)
- Ao contrário do Azure, onde os tipos de processadores do anfitrião estão selecionados para rácio de preço/desempenho melhor Olá, tipos de processador de Olá escolhidos para SAP HANA no Azure (instâncias de grande) são Olá efetuar mais elevado de linha de processador de Olá Intel E7v3 e E7v4.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>A executar várias instâncias de SAP HANA numa unidade de instância grande HANA
É possível toohost mais do que uma instância de SAP HANA Active Directory em unidades de instância grande HANA Olá. Ordem toostill fornecem capacidades de Olá de instantâneos de armazenamento e recuperação após desastre, este tipo de configuração exige um volume definido por instância. A partir de agora, unidades de instância grande HANA Olá podem subdivididas da seguinte forma:

- S72 S72m, S144, S192: Iniciar unidade em incrementos de 256 GB com Olá 256 GB mais pequeno. Incrementos diferentes como 256 GB, 512 GB e assim sucessivamente, podem ser combinados toohello máximo de memória de Olá da unidade de Olá.
- S144m e S192m: em incrementos de 256 GB com a unidade de menor de Olá 512 GB. Incrementos diferentes como 512 GB, 768 GB e assim sucessivamente, podem ser combinados toohello máximo de memória de Olá da unidade de Olá.
- Tipo de classe II: em incrementos de 512 GB com Olá mais pequeno de iniciar a unidade de 2 TB. Incrementos diferentes como 512 GB, 1 TB, 1,5 TB e assim sucessivamente, podem ser combinados toohello máximo de memória de Olá da unidade de Olá.

Alguns exemplos de executar várias instâncias de SAP HANA podem ter o seguinte aspeto:

| SKU | Tamanho da Memória | Tamanho de Armazenamento | Tamanhos com várias bases de dados |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1 x 768 GB HANA instância<br /> ou instância de 1 x 512 GB + 1 x 256 GB instância<br /> ou instâncias de 3 x 256 GB | 
| S72m | 768 GB | 3 TB | 3x512GB HANA instâncias<br />ou instância de 1 x 512 GB + 1 1 TB instância<br />ou instâncias de 6 x 256 GB<br />ou instância de 1x1.5 TB | 
| S192m | 4 TB | 16 TB | Instâncias de 8 x 512 GB<br />ou instâncias de 4 1 TB<br />ou instâncias de 4 x 512 GB + 2 1 TB instâncias<br />ou instâncias de 4 x 768 GB + instâncias de 2 x 512 GB<br />a instância de 1 4 TB ou |
| S384xm | 8 TB | 22 TB | Instâncias de 4 x 2 TB<br />ou instâncias de 2 4 TB<br />ou instâncias de 2, 3 TB + 1 x 2 TB instâncias<br />ou instâncias de 2x2.5 TB + 1 x 3 TB instâncias<br />a instância de 1 x 8 TB ou |


Obter ideia Olá. Existem certamente bem outras variações. 


## <a name="operations-model-and-responsibilities"></a>Modelo de operações e responsabilidades

serviço de Olá fornecido com o SAP HANA no Azure (instâncias de grande) está alinhado com os serviços do IaaS do Azure. Obter uma instância de instâncias de grande HANA com um sistema operativo instalado que está otimizada para SAP HANA. Tal como com as VMs IaaS do Azure, a maioria das tarefas de Olá da proteção de Olá SO, instalar software adicional que necessita, instalar HANA, operativo Olá SO e HANA e atualizar Olá SO e HANA é da responsabilidade do cliente. Microsoft não forçar atualizações do SO ou atualizações HANA no utilizador.

![Responsabilidades de SAP HANA no Azure (instâncias de grandes)](./media/hana-overview-architecture/image2-responsibilities.png)

Como pode ver no diagrama de Olá acima, o SAP HANA no Azure (instâncias de grande) é um infraestrutura de multi-inquilino como uma oferta de serviço. Como resultado, divisão Olá de responsabilidade se encontrando limites de infraestrutura de SO Olá, para Olá parte mais. Microsoft é responsável por todos os aspetos do serviço de Olá abaixo linha Olá do sistema de operativo Olá e é responsáveis acima linha Olá, incluindo o sistema de operativo Olá. Por isso, mais atuais no local métodos que pode ser empregar para gestão de compatibilidade, segurança, gestão de aplicações, base e SO podem continuar toobe utilizado. sistemas de Olá aparecem como se estão na sua rede no que diz respeito todos os.

No entanto, este serviço está otimizado para SAP HANA, pelo que existem áreas onde utilizador e a Microsoft precisam de capacidades de infraestrutura toowork toouse em conjunto Olá subjacente para obter os melhores resultados.

Olá a seguir lista fornece mais detalhes sobre cada uma das camadas de Olá e as suas responsabilidades:

**Redes:** Olá todas as redes internas para Olá instância grande carimbo de data / em execução SAP HANA, o respetivo armazenamento toohello acesso, a conectividade entre instâncias de Olá (para Escalamento horizontal e outras funções), horizontal toohello de conectividade e conectividade tooAzure em que camada da aplicação Olá SAP está alojada no Azure Virtual Machines. Também inclui conectividade WAN entre centros de dados do Azure para replicação de objetivos de recuperação após desastre. Todas as redes são particionadas por inquilino Olá e aplicou QOS.

**Armazenamento:** Olá virtualizar armazenamento particionado para todos os volumes necessários para servidores de SAP HANA Olá, bem como para instantâneos. 

**Servidores:** Olá dedicado servidores físicos toorun Olá SAP HANA DBs atribuído tootenants. Olá, servidores de Olá tipo posso de classe de SKUs são abstracted de hardware. Com estes tipos de servidores, a configuração do servidor Olá é recolhida e mantida em perfis, que podem ser movidas de um hardware físico para o hardware físico tooanother. Este tipo uma (manual) mudança de um perfil pelo operations pode ser comparado com um pouco tooAzure serviço autorrecuperação. servidores de Olá de Olá SKUs de classe de tipo II não são oferta essa uma capacidade.

**SDDC:** centros de software de gestão de Olá dados toomanage utilizado como entidades definidas por software. Permite recursos de toopool da Microsoft para escala, a disponibilidade e a motivos de desempenho.

**/ S:** Olá SO escolher (SUSE Linux ou Red Hat Linux) que está em execução nos servidores de Olá. as imagens de Olá SO que são fornecidos estão imagens Olá fornecidas pelo Olá individuais Linux fornecedor tooMicrosoft para fins de Olá da execução de SAP HANA. São necessário toohave uma subscrição com o fornecedor de Linux Olá para a imagem Olá específica com otimização de SAP HANA. As suas responsabilidades incluem a registar o fornecedor de SO Olá imagens Olá. Do ponto de Olá de handover pela Microsoft, é também responsável por quaisquer ainda mais a aplicação de patches do sistema de operativo Olá Linux. Esta aplicação de patches também inclui pacotes adicionais que poderão ser necessários para uma instalação de SAP HANA com êxito (consulte a documentação de instalação HANA e notas de SAP da tooSAP) e que não foi incluído pelo fornecedor Linux específico Olá no respetivo SAP HANA imagens de SO otimizadas. responsabilidade de Hello do cliente de Olá também inclui a aplicação de patches de Olá SO que está relacionada toomalfunction por otimização de Olá SO e o hardware de servidor específico do controladores toohello relacionados. Ou qualquer segurança ou aplicação de patches funcional de Olá SO. Responsabilidade do cliente é bem monitorização e planeamento de capacidade de:

- Consumo de recursos de CPU
- Consumo de memória
- Volumes toofree relacionados espaço em disco, IOPS e latência
- Tráfego de volume de rede entre a instância de grande HANA e a camada de aplicação do SAP

infraestrutura subjacente do Olá de instâncias de grande HANA fornece a funcionalidade cópia de segurança e restauro do volume de SO Olá. Utilizar esta funcionalidade também é da responsabilidade do cliente.

**Middleware:** Olá SAP HANA instância, principalmente. Administração, operações e monitorização são da responsabilidade do cliente. Não há funcionalidade desde que lhe permitem toouse instantâneos de armazenamento de cópia de segurança/restauro e objetivos de recuperação após desastre. Estas funcionalidades são fornecidas pela infraestrutura de Olá. No entanto, as suas responsabilidades também incluem conceber elevada disponibilidade ou recuperação de desastre com estas capacidades, tirar partido dos mesmos, monitorização e instantâneos de armazenamento tem sido executados com êxito.

**Dados:** os dados geridos pelo SAP HANA e outros dados, como cópias de segurança de partilhas de ficheiro ou ficheiros localizados em volumes. As suas responsabilidades incluem monitorização espaço livre em disco e gestão de conteúdo de Olá em volumes Olá, monitorização e a execução de cópias de segurança de volumes de disco e instantâneos de armazenamento com êxito Olá. No entanto, a execução com êxito dos sites de tooDR de replicação de dados é responsabilidade Olá da Microsoft.

**Aplicações:** Olá instâncias de aplicações SAP ou, em caso de aplicações não SAP, camada da aplicação Olá dessas aplicações. As suas responsabilidades incluem a implementação, administração, operações e monitorização dessas aplicações relacionadas com toocapacity planeamento de consumo de recursos de CPU, o consumo de memória, o consumo de armazenamento do Azure e o consumo de largura de banda de rede dentro do As VNets do Azure e as VNets do Azure tooSAP HANA no Azure (instâncias de grande).

**WANs:** Olá ligações estabelecer de implementações de tooAzure no local para cargas de trabalho. Todos os nossos clientes com instâncias de grande HANA utilizam Azure ExpressRoute para conectividade. Esta ligação não faz parte de Olá SAP HANA na solução do Azure (instâncias de grande), pelo que é responsável pela configuração de Olá desta ligação.

**Arquivo:** poderá preferir tooarchive cópias dos dados utilizando os suas próprias métodos em contas de armazenamento. Arquivar necessita de operações, os custos, conformidade e gestão. É responsável pela geração de cópias de arquivo e as cópias de segurança do Azure e armazene-os de forma em conformidade.

Consulte Olá [SLA para SAP HANA no Azure (instâncias de grande)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Dimensionamento

Dimensionamento para instâncias de grande HANA é não diferem Dimensionar para HANA em geral. Para existente e implementados sistemas, pretende toomove de outro tooHANA RDBMS, SAP fornece um conjunto de relatórios que são executadas em sistemas de SAP existentes. Se a base de dados de Olá tooHANA movido, estes relatórios verificar dados Olá e calcular os requisitos de memória para a instância do Olá HANA. Ler Olá segue SAP notas tooget obter mais informações sobre como toorun estes relatórios e como tooobtain das respetivas versões/patches mais recentes:

- [A nota #1793345 - Dimensionar para SAP Suite no HANA](https://launchpad.support.sap.com/#/notes/1793345)
- [SAP nota #1872170 - Suite HANA e S/4 HANA relatório de dimensionamento](https://launchpad.support.sap.com/#/notes/1872170)
- [A nota #2121330 - FAQ: SAP BW no HANA relatório de dimensionamento](https://launchpad.support.sap.com/#/notes/2121330)
- [SAP nota #1736976 - relatório de dimensionamento para BW no HANA](https://launchpad.support.sap.com/#/notes/1736976)
- [SAP nota #2296290 - novo relatório de dimensionamento para BW no HANA](https://launchpad.support.sap.com/#/notes/2296290)

Para implementações de campo verde, Sizer rápida SAP é requisitos de memória disponível toocalculate de implementação de Olá do software SAP HANA por cima do.

Requisitos de memória para HANA estão aumentar conforme o crescimentos de volume de dados, para que pretende toobe com suporte para Olá consumo de memória agora e ser capaz de toopredict aquelas que são curso toobe no Olá futuras. Com base nos requisitos de memória de Olá, pode mapear, em seguida, o pedido para um dos Olá HANA grande SKUs de instância.

## <a name="requirements"></a>Requisitos

Esta lista monta requisitos para executar o SAP HANA no Azure (instâncias superior).

**Microsoft Azure:**

- Uma subscrição do Azure que pode ser ligado tooSAP HANA no Azure (instâncias de grande).
- Contrato do suporte do Microsoft Premier. Consulte [2015553 de n. º de nota de suporte de SAP – SAP no Microsoft Azure: pré-requisitos do suporte](https://launchpad.support.sap.com/#/notes/2015553) para obter informações específicas relacionadas com toorunning SAP no Azure. Utilizar unidades de instância grande HANA com 384 e mais CPUs, terá também tooextend Olá tooinclude de contrato do suporte Premier resposta rápida do Azure (ARR).
- Deteção de instâncias de grande Olá HANA SKUs necessário depois de efetuar um dimensionamento exerce com SAP.

**Conectividade de rede:**

- Azure ExpressRoute no local tooAzure: tooconnect sua tooAzure de centro de dados no local, marca se tooorder, pelo menos, uma ligação de Gbps 1 do seu ISP. 

**Sistema operativo:**

- Licenças do SUSE Linux Enterprise Server 12 para aplicações SAP.

> [!NOTE] 
> Olá sistema de operativo disponibilizadas pela Microsoft não está registado no SUSE, nem está ligado com uma instância SMT.

- SUSE Linux subscrição gestão ferramenta (SMT) implementados no Azure numa VM do Azure. Isto fornece a capacidade de Olá para SAP HANA no Azure (instâncias de grande) toobe registado e respetivamente atualizado pelo SUSE (uma vez que não há nenhum acesso à internet no Centro de dados de instâncias de grande HANA). 
- Licenças do Red Hat Enterprise Linux 6.7 ou 7.2 para SAP HANA.

> [!NOTE]
> Olá sistema de operativo disponibilizadas pela Microsoft não está registado no Red Hat, nem é it ligado tooa Red Hat subscrição Manager instância.

- Red Hat subscrição Manager implementado no Azure numa VM do Azure. Olá Red Hat subscrição Manager permite Olá para SAP HANA no Azure (instâncias de grande) toobe registado e respetivamente atualizado pelo Red Hat (uma vez que não há nenhum acesso direto à internet de dentro do inquilino Olá implementado em Olá instância grande de Azure carimbo de data /).
- SAP requer toohave um suporte de contrato, bem como o seu fornecedor de Linux. Este requisito não é apagar pela solução de Olá do facto de instâncias de grande HANA ou Olá de que a executar Linux no Azure. Ao contrário com algumas das imagens de galeria do Azure de Linux Olá, taxa de serviço Olá não está incluída na oferta de soluções de Olá de instâncias de grande HANA. É, como um cliente toofulfill Olá requisitos do SAP sobre contratos de suporte com o distribuidor de Linux Olá.   
   - Para o SUSE Linux, procurar Olá requisitos de suporte de contrato no [1984787 de n. º de nota SAP - SUSE LINUX Enterprise Server 12: notas instalação](https://launchpad.support.sap.com/#/notes/1984787) e [&#1056161; nota SAP - SUSE prioridade suporte para aplicações SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Para Red Hat Linux, tem de toohave Olá subscrição correta níveis que incluem suporte e de serviço (atualizações de sistemas de operativos toohello de instâncias de grande HANA. Red Hat recomenda obter uma subscrição de "RHEL para SAP aplicações empresariais". Sobre o suporte e serviços, verifique [2002167 de n. º de nota SAP - Red Hat Enterprise Linux 7. x: instalação e a atualização](https://launchpad.support.sap.com/#/notes/2002167) e [1496410 de n. º de nota SAP - Red Hat Enterprise Linux 6. x: instalação e a atualização](https://launchpad.support.sap.com/#/notes/1496410) para detalhes.

**Base de dados:**

- As licenças e componentes de instalação de software para SAP HANA (plataforma ou enterprise edition).

**Aplicações:**

- As licenças e componentes de instalação de software para quaisquer aplicações SAP ligar tooSAP HANA e contratos de suporte SAP relacionados.
- Licenças e componentes de instalação de software para quaisquer aplicações SAP não utilizada na relação tooSAP HANA no ambiente do Azure (instâncias de grandes dimensões) e relacionadas com contratos de suporte.

**Competências:**

- Experiência e dados de conhecimento no IaaS do Azure e os respetivos componentes.
- Experiência e conhecimentos sobre a implementação da carga de trabalho do SAP no Azure.
- Instalação do SAP HANA certificados pessoal.
- SAP arquiteto competências toodesign elevada disponibilidade e recuperação após desastre em torno de SAP HANA.

**SAP:**

- Expectativas são de que já for um cliente SAP e tem um suporte de contrato com o SAP
- Especialmente para implementações em Olá classe II de tipo de instância SKUs de grande HANA, recomenda-se vivamente tooconsult com SAP em versões do SAP HANA e eventual configurações de hardware de cópia de segurança de escala de tamanho grande.


## <a name="storage"></a>Armazenamento

Olá esquema de armazenamento de SAP HANA no Azure (instâncias de grande) está configurada por SAP HANA na gestão de serviço do Azure através do SAP recomendado diretrizes, documentadas em Olá [os requisitos de armazenamento do SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) documento técnico.

Olá HANA instâncias grande Olá tipo posso classe vêm com o volume de memória de Olá quatro vezes como volume de armazenamento. Para o tipo de Olá classe II de unidades de instância grande HANA, armazenamento Olá não vai toobe mais de quatro vezes. unidades de Olá vêm com um volume, o que é dirigido para armazenar cópias de segurança de registos de transação de HANA. Encontrar mais detalhes em [como tooinstall e configurar o SAP HANA (instâncias de grande) no Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consulte Olá em termos de alocação de armazenamento, a tabela seguinte. tabela de Olá aproximadamente lista capacidade Olá para volumes diferentes Olá fornecido com unidades de instância grande HANA diferentes Olá.

| HANA grande instância SKU | Hana/dados | Hana/registo | Hana/partilhado | Hana / / cópia de segurança |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16,000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36,000 GB | 4100 GB | 2050 GB | 4100 GB |


Volumes implementados reais podem variar um pouco com base na implementação e a ferramenta de tamanhos de volume de Olá tooshow utilizados.

Se subdividir um SKU de instância grande HANA, alguns exemplos de peças de divisão possíveis deverá ter o seguinte aspeto:

| Partição de memória em GB | Hana/dados | Hana/registo | Hana/partilhado | Hana / / cópia de segurança |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Estes são números de volume aproximada que podem diferir ligeiramente com base na implementação e ferramentas utilizadas toolook em volumes Olá. Também existem outros tamanhos de partição thinkable, como 2,5 TB. Estes tamanhos de armazenamento deverá ser calculados com uma fórmula semelhante como utilizado para partições de Olá acima. termo Olá 'partitions' indicam que sistema de operativo Olá, memória ou recursos de CPU são de qualquer forma particionados. Indica apenas as partições de armazenamento para Olá diferentes HANA instâncias poderá toodeploy num único unidade instância grande HANA. 

Como um cliente pode ter precisa de mais armazenamento, terá de Olá possibilidade tooadd armazenamento toopurchase armazenamento adicional em unidades de 1 TB. Este armazenamento adicional pode ser adicionado como volume adicional ou pode ser utilizado tooextend um ou mais dos volumes existentes Olá. Não é possível toodecrease tamanhos de Olá de volumes de Olá como originalmente implementadas e principalmente documentado Olá tabelas acima. É também não nomes de Olá toochange possíveis dos volumes de Olá ou nomes de montagem. volumes de armazenamento Olá, tal como descrito acima são toohello anexado HANA instância de grandes unidades como NFS4 volumes.

Como um cliente pode escolher toouse instantâneos de armazenamento de cópia de segurança/restauro e desastre fins de recuperação. Obter mais detalhes sobre este tópico passo são detalhados no [SAP HANA (instâncias de grande) elevada disponibilidade e recuperação após desastre no Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Encriptação de dados inativos
armazenamento de Olá utilizado para instâncias de grande HANA permite a encriptação transparente de dados de Olá como são armazenados em discos de Olá. No momento da implementação de uma unidade de instância grande HANA, tiver Olá opção toohave este tipo de encriptação ativada. Também pode escolher toochange tooencrypted volumes após a implementação de Olá já. Mover Olá dos volumes de tooencrypted não encriptada é transparente e não necessita de um tempo de inatividade. 

Com Olá tipo posso classe SKUs de arranque de Olá Olá volume LUN é armazenado, são encriptados. Em caso de tipo de Olá classe II de SKUs de HANA grande instâncias, terá de arranque de Olá tooencrypt LUN com métodos de SO. 


## <a name="networking"></a>Redes

arquitetura de Olá de redes do Azure é uma implementação de toosuccessful de componente de chave das aplicações SAP HANA instâncias de grandes dimensões. Normalmente, SAP HANA em implementações do Azure (instâncias de grande) tem uma maior horizontal SAP com várias soluções SAP diferentes com diferentes tamanhos de bases de dados, o consumo de recursos de CPU e utilização da memória. Provavelmente não todos esses sistemas SAP baseiam SAP HANA, para que a sua horizontal SAP, provavelmente, seria uma versão híbrida que utiliza:

- Implementação de SAP sistemas no local. Devido a tootheir tamanhos, estes sistemas atualmente não podem ser alojados no Azure; um exemplo clássico seria um sistema de SAP ERP de produção em execução no Microsoft SQL Server (como base de dados de Olá) que necessita de mais CPU ou podem fornecer recursos de memória de VMs do Azure.
- Implementada com base em SAP HANA SAP sistemas no local.
- Sistemas SAP implementados em VMs do Azure. Estes sistemas ser desenvolvimento, teste, sandbox, ou instâncias de produção para qualquer uma das Olá SAP NetWeaver aplicações baseadas em que podem implementar com êxito no Azure (em VMs), com base no pedido de memória e o consumo de recursos. Estes sistemas também podem basear nas bases de dados como o SQL Server (consulte [1928533 de n. º de nota de suporte de SAP – aplicações SAP no Azure: os tipos de produtos suportados e VM do Azure](https://launchpad.support.sap.com/#/notes/1928533/E)) ou SAP HANA (consulte [SAP HANA certificadas IaaS as plataformas](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- Implementar servidores de aplicações SAP no Azure (em VMs) que tiram partido de SAP HANA no Azure (instância grande) no carimbos de data / instância grande de Azure.

Enquanto uma versão híbrida horizontal SAP (com quatro ou mais diferentes cenários de implementação) é típica, há muitos cenários de cliente de horizontal SAP completa em execução no Azure. Como VMs do Microsoft Azure são cada vez mais poderosas, é aumentar o número de Olá dos clientes mover todas as soluções de SAP no Azure.

Não é complicado Azure redes no contexto de Olá dos sistemas SAP implementado no Azure. Se baseia-se no Olá seguintes princípios:

- Redes virtuais do Azure (VNets) necessário toobe ligado toohello circuito do ExpressRoute do Azure que estabelece ligação rede tooon local.
- Um circuito de ExpressRoute ligar tooAzure no local, normalmente, deve ter uma largura de banda de 1 Gbps ou superior. Esta largura de banda mínima permite largura de banda suficiente para transferir dados entre sistemas no local e em execução em VMs do Azure (bem como os sistemas de tooAzure de ligação dos utilizadores finais no local).
- Todos os sistemas de SAP toobe do Azure é necessário configurar as VNets do Azure toocommunicate entre si.
- Active Directory e DNS alojadas no local são expandidas no Azure através do ExpressRoute do local.


> [!NOTE] 
> A partir de um ponto de vista faturação, apenas uma única subscrição do Azure pode ser ligada a apenas tooone único inquilino num carimbo de instância grande numa região do Azure específico e, por outro lado pode ser associado um inquilino de carimbo de grande instância único apenas tooone subscrição do Azure. Este facto é tooany não diferente outros objetos sujeito a faturação no Azure

Resulta na toobe inquilino individual implementar SAP HANA no Azure (instâncias de grande) em várias regiões do Azure diferentes, implementados em Olá carimbo de instância de grandes dimensões. No entanto, pode executar ambos em Olá mesma subscrição do Azure desde que estas instâncias fazem parte do Olá SAP mesmo horizontal. 

> [!IMPORTANT] 
> Apenas a implementação de gestão de recursos do Azure é suportada com SAP HANA no Azure (instâncias de grande).

 

### <a name="additional-azure-vnet-information"></a>Informações adicionais de VNet do Azure

Na ordem tooconnect tooExpressRoute uma VNet do Azure, tem de ser criado um gateway do Azure (consulte [sobre gateways de rede virtual para o ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Um gateway do Azure pode ser utilizado com o ExpressRoute tooan infraestrutura fora do Azure (ou carimbo de instância do Azure grande tooan), ou tooconnect entre as VNets do Azure (consulte [configurar uma ligação VNet a VNet para o Resource Manager com o PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Pode ligar Olá gateway do Azure tooa máximo quatro ligações ExpressRoute diferentes, desde que essas ligações são feitos routers MS Enterprise contornos (MSEE) diferentes.  Para obter mais informações, consulte [infraestrutura de SAP HANA (instâncias de grandes dimensões) e a conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Olá débito fornece um gateway do Azure é diferente para ambos os casos de utilização (consulte [sobre o Gateway de VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). débito máximo de Olá, pode realizar com um gateway de VNet é de 10 Gbps, através de uma ligação ExpressRoute. Tenha em atenção que a copiar ficheiros entre uma VM do Azure que reside numa VNet do Azure e um sistema local (como uma sequência de cópia única) não conseguir débito total do Olá de SKUs de gateway diferentes Olá. tooleverage Olá concluída largura de banda do gateway de VNet Olá, tem de utilizar vários fluxos ou cópia de ficheiros diferente em fluxos paralelos de um único ficheiro.


### <a name="networking-architecture-for-hana-large-instances"></a>Arquitetura de rede para instâncias de grande HANA
Olá arquitetura de rede para instâncias de grande HANA conforme mostrado abaixo, pode ser separado em quatro partes distintas:

- Redes no local e tooAzure de ligação do ExpressRoute. Esta parte é o domínio de clientes Olá e tooAzure ligado através do ExpressRoute. Este processo faz parte de Olá na parte inferior direita de Olá de gráficos Olá abaixo.
- Funcionamento em rede do Azure como brevemente discutido acima com as VNets do Azure, novamente com gateways. Trata-se de uma área onde precisa de estruturas de adequado toofind Olá para os requisitos de aplicações, segurança e os requisitos de conformidade. Utilizando as instâncias grande HANA é outro ponto de consideração em termos de número de VNets e o Azure toochoose de SKUs de gateway do. Este processo faz parte de Olá no canto superior direito de Olá de gráficos Olá.
- Conectividade de instâncias de grande HANA através de tecnologia de ExpressRoute para o Azure. Esta peça é implementada e processada pela Microsoft. Tudo o que precisa toodo como um cliente é tooprovide alguns intervalos de endereços IP e após a implementação de Olá dos seus ativos em instâncias de grande HANA ligar Olá ExpressRoute circuito toohello VNet(s) do Azure (consulte [infraestrutura de SAP HANA (instâncias de grandes dimensões) e conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Funcionamento em rede em instâncias de grande HANA, que é principalmente transparente, para, como um cliente.

![VNet do Azure ligado tooSAP HANA no Azure (instâncias de grandes dimensões) e no local](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

facto de Olá que utilize instâncias HANA grande não altera Olá requisito tooget seus recursos no local ligados através do ExpressRoute tooAzure. Também não altera requisito Olá para ter uma ou várias VNets que executar as VMs do Azure de Olá que camada da aplicação Olá anfitrião que liga as instâncias HANA toohello alojadas em unidades de instância grande HANA. 

implementações de tooSAP de diferença de Olá puro no Azure, vem com factos Olá que:

- unidades de instância grande HANA Olá do seu inquilino do cliente estão ligadas através de outro circuito do ExpressRoute para o seu VNet(s) do Azure. Em condições de carga tooseparate de ordem, Olá local tooAzure ligações do VNets ExpressRoute e ligações entre as VNets do Azure e instâncias HANA grandes não partilham Olá mesmo routers.
- perfil de carga de trabalho de Olá entre a camada da aplicação Olá SAP e Olá HANA instância é uma natureza diferente do número de pedidos pequeno e rajada como dados transferidos (conjuntos de resultados) de SAP HANA na camada da aplicação Olá.
- Olá arquitetura de aplicações SAP é mais sensível toonetwork latência que os cenários típicos onde os dados obtém trocados entre no local e o Azure.
- gateway de VNet Olá tem, pelo menos, duas ligações ExpressRoute e ambas as ligações partilham a largura de banda máxima Olá para dados recebidos do gateway de VNet Olá.

Latência de rede de Olá experiente entre as VMs do Azure e HANA grandes unidades de instância pode ser superior a uma típica latência reportadas round-trip de rede de VM para VM. Depende de Olá região do Azure, os valores de Olá medidos podem exceder latência do 0.7 ms de Olá reportadas round-trip classificada como abaixo média [1100926 de n. º de nota SAP - FAQ: desempenho de rede](https://launchpad.support.sap.com/#/notes/1100926/E). Contudo clientes baseados em SAP HANA produção SAP aplicações muito com êxito no SAP HANA grande instâncias implementadas. os clientes de Olá que implementado comunicadas excelente melhoramentos ao executar as aplicações SAP no SAP HANA utilizar unidades de instância grande HANA. Contudo deverá testar cuidadosamente os processos empresariais no Azure HANA grande instâncias.
 
Na ordem tooprovide determinista latência da rede entre as VMs do Azure e a instância de grande HANA, é essencial escolher Olá Olá SKU de Gateway de VNet do Azure. Ao contrário de padrões de tráfego de Olá entre no local e as VMs do Azure, o padrão de tráfego de Olá entre as VMs do Azure e instâncias de grande HANA pode desenvolver bursts pequenos mas elevadas de pedidos de e toobe de volumes de dados transmitidos. Na ordem toohave essas bursts processados, recomendamos vivamente utilização Olá de Olá UltraPerformance SKU de Gateway. Para a classe de II de tipo de instância SKUs de grande HANA Olá, a utilização de Olá do gateway de UltraPerformance Olá SKU como Gateway de VNet do Azure é obrigatória.  

> [!IMPORTANT] 
> Fornecido Olá geral tráfego de rede entre camadas de base de dados e aplicação de SAP Olá Olá apenas HighPerformance ou gateway UltraPerformance SKUs para VNets é suportada para ligar tooSAP HANA no Azure (instâncias de grande). A instância do tipo II SKUs HANA grande, apenas Olá UltraPerformance SKU de Gateway é suportada como Gateway de VNet do Azure.



### <a name="single-sap-system"></a>Sistema SAP única

infraestrutura no local de Olá mostrada acima está ligada através do ExpressRoute para o Azure e Olá circuito ExpressRoute liga-se para um Router de limite do Microsoft Enterprise (MSEE) (consulte [descrição geral técnica do ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Depois de estabelecido, essa rota liga-se na estrutura principal do Microsoft Azure de Olá, e todas as regiões do Azure estão acessíveis.

> [!NOTE] 
> Para executar SAP landscapes no Azure, ligar toohello MSEE mais próximo toohello região do Azure na horizontal SAP Olá. Azure instância grande carimbos de data / está ligados através de dedicado MSEE dispositivos toominimize latência de rede entre as VMs do Azure no IaaS do Azure e a instância grande carimbos de data /.

Olá gateway de VNet para Olá VMs do Azure, instâncias de aplicações SAP, de alojamento está ligado toothat circuito do ExpressRoute e, hello mesma VNet tooa ligado separado Router MSEE dedicado tooconnecting tooLarge instância carimbos de data /.

Este é um exemplo simples de um único sistema SAP, onde hello camada de aplicação do SAP está alojada no Azure e a base de dados de SAP HANA Olá é executado no SAP HANA no Azure (instâncias de grande). pressuposto Olá é essa Olá VNet gateway largura de banda de 2 Gbps ou 10 Gbps débito não representa um estrangulamento.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Vários sistemas SAP ou grandes sistemas SAP

Se vários SAP sistemas ou grandes SAP sistemas são implementados ligar tooSAP HANA no Azure (instâncias de grande) &#39; débito de Olá s tooassume razoável do gateway de VNet Olá pode tornar-se um engarrafamento. Nesse caso, terá de camadas de aplicação de Olá toosplit em várias VNets do Azure. Também poderá ser recommendable toocreate VNets especiais que se ligam instâncias grande tooHANA para casos como:

- Efetuar cópias de segurança diretamente a partir de Olá HANA instâncias instâncias grande HANA tooa VM no Azure que aloja partilhas de NFS
- Copiar as cópias de segurança grandes ou outros ficheiros de HANA grandes unidades toodisk espaço de instância de geridas no Azure.

Utilizar VNets separadas que anfitrião VMs que gerir o armazenamento de Olá evita impacto por ficheiros grandes ou transferência de dados da instâncias grande HANA tooAzure no Olá Gateway de VNet que serve de VMs de Olá camada da aplicação Olá SAP em execução. 

Para uma arquitetura de rede mais escalável:

- Tire partido de várias VNets do Azure para uma camada de aplicação de SAP única e superior.
- Implementar uma VNet do Azure separado para cada sistema SAP implementado, toocombining em comparação com estes sistemas SAP sub-redes separadas em Olá mesma VNet.

 Uma arquitetura de rede mais dimensionável para SAP HANA no Azure (instâncias de grande):

![Implementar a camada de aplicação de SAP através de várias VNets do Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Implementar a camada da aplicação Olá SAP ou componentes, através de várias VNets do Azure conforme mostrado acima, introduzida overhead de latência de obrigatório que ocorreram durante a comunicação entre aplicações Olá alojado as vnets do Azure. Por predefinição, o tráfego de rede Olá entre as VMs do Azure localizadas no diferentes VNets encaminhar através de Olá routers MSEE nesta configuração. No entanto, dado que Setembro de 2016 este encaminhamento pode ser otimizado. Olá toooptimize de forma e diminuir a latência de Olá na comunicação entre duas VNets está por peering as VNets do Azure dentro Olá mesma região. Mesmo que esses VNets estão em subscrições diferentes. Utilizar o Azure VNet peering, comunicação de Olá entre VMs em duas VNets do Azure diferente pode utilize Olá rede Azure principal toodirectly comunicam entre si. Deste modo, latência semelhante que mostra como se Olá VMs seria no Olá mesma VNet. Enquanto que o tráfego, endereçamento intervalos de endereços IP que estão ligados através do gateway de VNet do Azure Olá, é encaminhado através de Olá gateway de VNet individual de Olá VNet. Pode obter detalhes sobre o Azure VNet peering no artigo Olá [o VNet peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Encaminhamento no Azure

Existem duas considerações de encaminhamento de rede importantes para SAP HANA no Azure (instâncias de grande):

1. SAP HANA no Azure (instâncias de grande) só pode ser acedido por VMs do Azure na ligação do ExpressRoute Olá dedicado; não diretamente a partir do local. Alguns clientes de administração e todas as aplicações que necessitam acesso direto, tais como o SAP solução Manager em execução no local, não é possível ligar a base de dados do toohello SAP HANA.

2. SAP HANA nas unidades do Azure (instâncias de grande) têm um endereço IP atribuído do endereço de conjunto de IP do servidor de Olá intervalo, como cliente Olá submetido (consulte [infraestrutura de SAP HANA (instâncias de grandes dimensões) e a conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes).  Este endereço IP é acessível através de Olá Azure ExpressRoute que liga as VNets do Azure tooHANA no Azure (instâncias de grandes dimensões) e subscrições. Olá endereço IP atribuído fora desse intervalo de endereços do conjunto de IP do servidor lhe esteja diretamente atribuído toohello unidade de hardware e não é NAT'ed já foi caso Olá em implementações de primeiro Olá desta solução. 

> [!NOTE] 
> Se precisar de tooconnect tooSAP HANA no Azure (instâncias de grande) num _do armazém de dados_ cenário, onde as aplicações e/ou os utilizadores finais têm de tooconnect toohello SAP HANA da base de dados (diretamente em execução), tem de ser outro componente de rede utilizado: de dados de proxy inverso tooroute, tooand do. Por exemplo, F5 BIG-IP, NGINX com o Gestor de tráfego seja implementado no Azure como uma solução de encaminhamento de tráfego/firewall virtual.

### <a name="internet-connectivity-of-hana-large-instances"></a>Acesso à Internet de instâncias de grande HANA
Instâncias de grande HANA não tem conectividade internet direta. Isto é restringir as capacidades para, por exemplo, registar imagem do SO Olá diretamente com o fornecedor de SO Olá. Por conseguinte, poderá ser necessário toowork com servidor SLES SMT local ou o Gestor de subscrição de RHEL

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Encriptação de dados entre as VMs do Azure e instâncias de grande HANA
Dados transferidos entre instâncias de grande HANA e as VMs do Azure não estão encriptados. No entanto, puramente para a troca de Olá entre Olá lado HANA DBMS e as aplicações de JDBC/ODBC com base pode ativar a encriptação de tráfego. Referência [esta documentação por SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Utilizar unidades de instância grande HANA em várias regiões

Poderá ter outro toodeploy motivos SAP HANA no Azure (instâncias de grande) em várias regiões do Azure, para além de recuperação após desastre. Talvez pretenda tooaccess HANA instâncias de grandes dimensões de cada uma das VMs Olá implementadas na Olá VNets diferentes regiões Olá. Uma vez que os endereços IP de Olá atribuídos toohello diferentes unidades de instâncias de grande HANA não são propagadas para além de Olá as VNets do Azure (que estão ligados diretamente através do respetivas instâncias de toohello gateway), existe uma pequena alterar toohello conceção de VNet introduzida acima: um Gateway de VNet do Azure pode processar quatro circuitos do ExpressRoute diferentes fora MSEEs diferentes e cada VNet que está ligado tooone de carimbos de instância grande Olá pode ser ligados toohello instância grande carimbo de data / noutra região do Azure.

![As VNets do Azure ligado tooAzure instância grande carimbos de data / em diferentes regiões do Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Olá acima mostra a figura como Olá diferentes as VNets do Azure nas regiões são ligados tootwo diferentes circuitos do ExpressRoute que são utilizados tooconnect tooSAP HANA no Azure (instâncias de grande) em ambas as regiões do Azure. ligações de Olá recentemente introduzida são as linhas de vermelho retangular Olá. Com estas ligações, fora Olá as VNets do Azure, VMs de Olá em execução desses VNets podem aceder a cada uma das unidades Olá diferentes instâncias grande HANA implementadas em duas regiões de Olá. Como ver em gráficos de Olá acima, presume-se que tem duas ligações ExpressRoute do local toohello duas regiões do Azure; recomendado por motivos de recuperação após desastre.

> [!IMPORTANT] 
> Se forem utilizados vários circuitos ExpressRoute, prefixação como caminho e as definições de BGP de preferência Local devem ser utilizado tooensure adequada de encaminhamento de tráfego.


