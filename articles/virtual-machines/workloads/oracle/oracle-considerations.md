---
title: "soluções de aaaOracle no Microsoft Azure | Microsoft Docs"
description: "Saiba mais sobre as configurações suportadas e limitações das soluções de Oracle no Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Soluções de Oracle e a respetiva implementação no Microsoft Azure
Este artigo aborda as informações necessária toosuccesfully implementar várias soluções de Oracle no Microsoft Azure. Estas soluções são baseadas em imagens da Máquina Virtual publicadas pelo Oracle na Olá Azure Marketplace. tooget uma lista de imagens atualmente disponíveis, execute Olá os seguintes comandos:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
A partir da lista de Olá 6-16-2017 das imagens são seguinte Olá:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Estas imagens são consideradas "Traga a sua própria licença" e como tal será apenas cobrada para computação, armazenamento e os custos de funcionamento em rede tarifas executando uma VM.  Presume-se estão devidamente licenciados toouse Oracle software e de que tem um contrato de suporte atual no local com o Oracle. Oracle tem garantida mobilidade de licenças de tooAzure no local. Consulte Olá publicado [Oracle e Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) nota para obter detalhes sobre mobilidade de licenças. 

Indivíduos também podem escolher toobase as soluções de imagens personalizadas que criar a partir do zero no Azure ou carregar um imagens personalizadas dos respetivos ambientes no local no.

## <a name="support-for-jd-edwards"></a>Suporte para JD Edwards
Nota de suporte de tooOracle de acordo com [2178595.1 de ID do documento](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne verions 9.2 e superior, são suportadas em **qualquer público na nuvem a oferta de** que satisfaz as respetivas específicos `Minimum Technical Requirements` (MTR).  Terá de toocreate imagens personalizadas que cumprem as respetivas especificações MTR para compatibilidade de aplicações do SO e software. 

## <a name="oracle-database-virtual-machine-images"></a>Imagens de máquina virtual de base de dados Oracle
Oracle suporta edições Oracle DB 12.1 Standard e Enterprise em execução no Azure em imagens da máquina virtual com base no Oracle Linux.  Para Olá melhor desempenho para cargas de trabalho de produção de Oracle DB no Azure, ser se tooproperly tamanho Olá VM imagem e utilizar discos geridos que sejam copiados pelo armazenamento Premium. Para obter instruções sobre como tooquickly obtêm uma base de dados Oracle e em execução no Azure utilizando Olá Oracle publicado a imagem de VM, [tente instruções do guia de introdução do Oracle DB de Olá](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Opções de configuração de disco ligado

Discos ligados dependem Olá serviço de armazenamento de Blobs do Azure. Cada disco padrão é capaz de um máximo de teórico de aproximadamente 500 operações de entrada/saída por segundo (IOPS). A nossa oferta do disco premium preferido para cargas de trabalho de base de dados de elevado desempenho e pode obter uma cópia de segurança too5000 IOps por disco. Apesar de poder utilizar tem de se de que cumpre o desempenho de um único disco - pode melhorar o desempenho de IOPS Efetivo Olá se utilizar vários discos ligados, distribuídos a base de dados por-los e, em seguida, utilize a gestão de armazenamento automática da Oracle (ASM). Consulte [descrição geral de armazenamento automática Oracle](http://www.oracle.com/technetwork/database/index-100339.html) para obter mais informações específicas de ASM do Oracle. Para obter um exemplo de como tooinstall e configurar Oracle ASM numa VM com Linux do Azure – pode tentar Olá [instalar e configurar Oracle automatizada gestão de armazenamento](configure-oracle-asm.md) tutorial.

### <a name="oracle-realtime-application-cluster-rac"></a>Cluster de aplicação do Oracle em tempo real (RAC)
Oracle RAC é concebida toomitigate Olá falha de um único nó uma configuração de cluster de vários nós no local.  Baseia-se em duas tecnologias no local que não são ambientes de nuvem pública da escala toohyper nativa: multicast rede e de disco partilhado. Existem soluções de terceiros criadas pelas empresas [como FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) que emulam estas tecnologias se precisar de toodeploy RAC Oracle no Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Considerações de recuperação após desastre e disponibilidade elevada
Quando utilizar bases de dados Oracle no Azure, é responsável por implementar uma elevada disponibilidade e após desastre recuperação solução tooavoid qualquer período de inatividade. 

Elevada disponibilidade e recuperação após desastre para Oracle da base de dados Enterprise Edition (sem RAC) no Azure pode ser conseguida utilizando [Data Guard, Active Directory Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html), ou [Oracle Golden porta](http://www.oracle.com/technetwork/middleware/goldengate), com duas bases de dados duas máquinas virtuais separadas. Ambas as máquinas virtuais devem ser na Olá mesmo [rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure poderem aceder ao entre si através de endereço IP de persistente privado de Olá.  Além disso, recomendamos que a colocação de máquinas virtuais Olá no Olá tooallow tooplace do Azure do conjunto de disponibilidade do mesma-os em separado domínios de falha e domínios de atualização.  Se pretender que georredundância toohave - podem ter estas duas bases de dados são replicados entre duas regiões diferentes e ligar duas instâncias de Olá com um Gateway de VPN.

Temos um tutorial "[DataGuard Oracle de implementar no Azure](configure-oracle-dataguard.md)" que explica como Olá configuração básica procedimento tootrial isto no Azure.  

Com o Oracle Data Guard, elevada disponibilidade pode ser conseguida com uma base de dados primária em máquinas virtuais, uma base de dados (modo de espera) secundário na outra máquina virtual e replicação unidirecional configurar entre eles. resultado de Olá é acesso de leitura toohello cópia da base de dados de Olá. Com o Oracle GoldenGate, pode configurar a replicação bidirecional entre duas bases de dados Olá. toolearn como tooset configurar uma solução de elevada disponibilidade para as bases de dados a utilizar estas ferramentas, consulte [Active Directory Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) e [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentação do Web site do Olá Oracle. Se o precisa de leitura e escrita acesso toohello cópia da base de dados de Olá, pode utilizar [Active Directory Oracle Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Temos um tutorial "[GoldenGate Oracle de implementar no Azure](configure-oracle-golden-gate.md)" que explica como Olá seup básico procedimento tootrial isto no Azure.

Apesar de ter uma solução HA e DR criada no Azure, quer tooensure tiver uma estratégia de cópia de segurança no local toorestore a base de dados.  Temos um tutorial [cópia de segurança e recuperar uma base de dados Oracle](oracle-backup-recovery.md) que explica como procedimento de básico Olá para estabelecer uma cópia de segurança consistant.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Imagens da máquina virtual Oracle WebLogic Server
* **Clustering só é suportado na edição Enterprise.** São licenciados toouse WebLogic clustering apenas quando utilizar Olá Enterprise Edition do WebLogic Server. Não utilize o clustering com WebLogic Server Standard Edition.
* **Não é suportado multicast do UDP.** Azure suporta UDP unicasting, mas não utilizar multicast ou difusão. O servidor de WebLogic é capaz de toorely nas capacidades do Azure UDP unicast. Para melhor resultados depender UDP unicast, recomendamos que o tamanho do cluster Olá WebLogic seja mantida estático, ou ser mantidas com mais do que 10 incluídos no cluster de Olá os servidores geridos.
* **Servidor WebLogic espera Olá de toobe portas públicas e privadas mesmo para T3 de acesso (por exemplo, ao utilizar a Enterprise JavaBeans).** Considere um cenário de várias camado onde uma aplicação de camada (EJB) do serviço está em execução num cluster de servidores de WebLogic constituídas por duas ou mais VMs, numa vNet com o nome **SLWLS**. escalão de cliente de Olá está numa sub-rede diferente no Olá mesma vNet, executar um programa de Java simple toocall EJB na camada de serviço Olá a tentar. Porque se encontra a camada de serviço do tooload necessário balanceamento Olá, um ponto de final público com balanceamento de carga tem de toobe criado para Olá máquinas virtuais no Olá cluster WebLogic Server. Se uma porta privada Olá que especificou é diferente da porta pública de Olá (por exemplo, 7006:7008), ocorre um erro, tais como o seguinte Olá:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Isto acontece porque para qualquer T3 o acesso remoto, WebLogic Server espera porta de Balanceador de carga Olá e Olá WebLogic gerido servidor porta toobe Olá mesmo. Olá acima maiúsculas e minúsculas, cliente Olá está a aceder a porta 7006 (porta de Balanceador de carga Olá) e servidor gerido Olá está a escutar 7008 (Olá uma porta privada). Esta restrição se aplica apenas T3 acesso, não HTTP.

   tooavoid este problema, utilize uma das seguintes soluções de Olá:

  * Utilize Olá mesmo privada e números de porta pública de carga com balanceamento de pontos finais dedicados tooT3 acesso.
  * Inclua Olá parâmetro JVM os seguintes quando iniciar WebLogic Server:

         -Dweblogic.rjvm.enableprotocolswitch=true

Para informações relacionadas, consulte o artigo BDC **860340.1** em <http://support.oracle.com>.

* **Dinâmica clustering e limitações de balanceamento de carga.** Suponha que pretende toouse um cluster dinâmico no servidor WebLogic e expô-la através de um único e público com balanceamento de carga ponto final no Azure. Isto pode ser efetuado desde que utilizar um número de porta fixo para cada um dos Olá geridos servidores (não dinamicamente atribuídos de um intervalo) e não se iniciam mais servidores geridos que existem máquinas administrador Olá está a controlar (ou seja, não mais do que um gerido servidor por virt o ual máquina). Se a configuração resulta em mais servidores de WebLogic sejam iniciados que existem máquinas virtuais (ou seja, em que várias partilha de instâncias de servidor WebLogic hello mesma máquina virtual), então, não é possível mais do que um essas instâncias de servidor WebLogic servidores tooa de toobind indicado o número de porta – Olá outros nessa máquina virtual irão falhar.

   No Olá por outro lado, se configurar Olá admin servidor tooautomatically atribuir números de porta exclusivo tooits geridos servidores, em seguida, o balanceamento de carga não é possível porque o Azure não suporta o mapeamento de uma única porta pública toomultiple privada portas, tal como seria necessário para esta configuração.
* **Várias instâncias do Weblogic Server numa máquina virtual.** Dependendo dos requisitos da sua implementação, que pode considerar a opção de Olá de várias instâncias do WebLogic Server em execução no Olá mesma máquina virtual, se a máquina virtual de Olá é suficientemente grande. Por exemplo, uma máquina virtual de tamanho médio, que contém dois núcleos, pode escolher toorun duas instâncias do WebLogic Server. Tenha em atenção contudo que recomendamos que evite pontos únicos de falha a introduzir na sua arquitetura que seria caso Olá se tiver utilizado apenas uma máquina virtual que está a executar várias instâncias do WebLogic Server. Utilizar, pelo menos, duas máquinas virtuais pode ser uma abordagem melhor e cada uma dessas máquinas virtuais, em seguida, pode executar várias instâncias do WebLogic Server. Cada um destes instâncias de servidor WebLogic ainda foi possível parte Olá mesmo cluster. Tenha em atenção, no entanto, atualmente não é possível pontos finais de toouse balancear tooload do Azure que sejam expostos pelo implementações deste tipo WebLogic Server dentro Olá mesma máquina virtual, porque o Balanceador de carga do Azure requer Olá servidores com balanceamento de carga toobe distribuído em máquinas virtuais exclusivas.

## <a name="oracle-jdk-virtual-machine-images"></a>Imagens da máquina virtual JDK Oracle
* **JDK 6 e 7 atualizações mais recentes.** Enquanto Recomendamos que utilize a versão mais recente público, suportados Olá do Java (atualmente Java 8), Azure também disponibiliza JDK 6 e 7 imagens. Destina-se para aplicações antigas que ainda não foram toobe pronto atualizado tooJDK 8. Durante as atualizações tooprevious JDK imagens já não poderão ser público geral toohello disponível, fornecido Olá Microsoft parceria com Oracle, Olá JDK 6 e 7 imagens fornecidas pelo Azure são pretendido toocontain uma atualização mais recente do não público que normalmente é oferecida pelo Oracle tooonly a um grupo de Oracle do suportada clientes. Novas versões das imagens JDK Olá serão disponibilizadas ao longo do tempo com versões atualizadas do JDK 6 e 7.

   Olá JDK disponível neste JDK 6 e 7 imagens e as máquinas virtuais de Olá e imagens derivadas deles, só podem ser utilizadas no Azure.
* **JDK de 64 bits.** imagens da máquina virtual Oracle WebLogic Server Olá e imagens da máquina virtual Olá Oracle JDK fornecidas pelo Azure contêm as versões de 64 bits de Olá do Windows Server e Olá JDK.

## <a name="next-steps"></a>Passos seguintes
Tem agora uma descrição geral das soluções de Oracle atual no Microsoft Azure. O próximo passo é toogo e implementar a sua primeira base de dados Oracle no Azure.
- Tente Olá [criar uma base de dados Oracle no Azure](oracle-database-quick-create.md) tooget tutorial foi iniciado.
