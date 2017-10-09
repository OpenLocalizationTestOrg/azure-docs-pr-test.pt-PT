---
title: "aaaProtect uma implementação de aplicação multicamada SAP NetWeaver utilizando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooprotect SAP NetWeaver implementações de aplicações utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Proteger uma implementação de aplicação multicamada SAP NetWeaver utilizando o Azure Site Recovery

A maioria das implementações de grande e média da SAP têm algum tipo de solução de recuperação após desastre.  importância Olá das soluções de recuperação após desastre robustas e testable aumentou como mais empresas de núcleos os processos são movidos tooapplications, tais como o SAP.  O Azure Site Recovery foi testadas e integradas com aplicações SAP e excede as capacidades de Olá da maioria das soluções de recuperação após desastre no local, um custo inferior total de propriedade (TCO) que soluções concorrentes.
Com o Azure Site Recovery, pode:
* Ative a proteção das aplicações SAP NetWeaver e NetWeaver de produção em execução no local, através da replicação tooAzure de componentes.
* Ative a proteção das aplicações SAP NetWeaver e NetWeaver de produção com o Azure, através da replicação de componentes tooanother datacenter do Azure.
* Simplifica a migração de nuvem, utilizando a recuperação de sites toomigrate tooAzure de implementação do SAP.
* Simplifique as atualizações, testes e protótipos de projetos SAP ao criar um clone de produção a pedido para testar aplicações SAP.

Este artigo descreve como tooprotect SAP NetWeaver implementações de aplicações utilizando [do Azure Site Recovery](site-recovery-overview.md). Este artigo abrange as melhores práticas de Olá para proteger uma implementação de SAP NetWeaver de três camadas no Azure através da replicação tooanother datacenter do Azure utilizando o Azure Site Recovery, cenários de Olá suportado e às configurações, e como as ativações pós-falha de tooperform, ambos de teste as ativações pós-falha (simulações de recuperação após desastre) e as ativações pós-falha real.


## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, certifique-se de que compreende seguinte Olá:

1. [Replicar tooAzure uma máquina virtual](azure-to-azure-walkthrough-enable-replication.md)
2. Como demasiado[estruturar uma rede de recuperação](site-recovery-azure-to-azure-networking-guidance.md)
3. [Fazer uma tooAzure de ativação pós-falha de teste](azure-to-azure-walkthrough-test-failover.md)
4. [Fazer uma tooAzure de ativação pós-falha](site-recovery-failover.md)
5. Como demasiado[replicar um controlador de domínio](site-recovery-active-directory.md)
6. Como demasiado[replicar do SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Cenários suportados
Com o Azure Site Recovery pode implementar uma solução de recuperação após desastre para Olá os seguintes cenários:
* Sistemas SAP em execução no datacenter do Azure um replicar tooanother datacenter do Azure (DR do Azure para o Azure), como criado [aqui](https://aka.ms/asr-a2a-architecture).
* Sistemas SAP em execução nos servidores do VMWare (ou físico) no local replicação site tooa DR num datacenter do Azure (VMware para o Azure DR), que requer alguns componentes adicionais conforme criado [aqui](https://aka.ms/asr-v2a-architecture).
* Sistemas SAP em execução no Hyper-V no local replicação site tooa DR num datacenter do Azure (Hyper-V para Azure DR), que requer alguns componentes adicionais conforme criado [aqui](https://aka.ms/asr-h2a-architecture).

Este documento utiliza funcionalidades de recuperação de desastre SAP Olá primeiro maiúsculas - DR do Azure para o Azure - toodemonstrate do Azure Site Recovery. Como a replicação do Azure Site Recovery desconhece de aplicação, o processo de Olá descrito é toohold esperada, bem como outros cenários.

### <a name="required-foundation-services"></a>Serviços necessários foundation
Neste cenário de documentação todos os foi implementado com Olá serviços foundation implementados os seguintes:
* ExpressRoute ou de Site para Site rede privada Virtual (VPN)
* Servidor de pelo menos um controlador de domínio do Active Directory e DNS em execução no Azure

Recomenda-se que essa infraestrutura Olá acima é estabelecida toodeploying anterior do Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Implementação de aplicação de SAP típica
Normalmente, implementar clientes SAP grande entre 6 aplicações SAP individuais too20.  A maioria destas aplicações baseiam-se no motores de Olá SAP NetWeaver ABAP ou Java.  Suportar estas aplicações de NetWeaver core é muitas mais pequenos motores de autónoma de SAP não NetWeaver específico e, normalmente, algumas aplicações não SAP.  

É fundamental tooinventory todas as Olá SAP aplicações em execução num horizontal e toodetermine Olá modo de implementação (camada 2 ou 3 camadas), versões, patches, tamanhos, churn taxas e requisitos de persistência de disco.

![Implementação padrão](./media/site-recovery-sap/sap-typical-deployment.png)

camada de persistência de base de dados SAP Olá deve ser protegida através de ferramentas DBMS nativas Olá como AlwaysOn do SQL Server, Oracle DataGuard ou HANA replicação do sistema. camada de cliente Olá não é também protegida pelo Azure Site Recovery, mas é importante tooconsider tópicos que afetam esta camada, tais como o atraso de propagação de DNS, segurança e acesso remoto toohello DR Centro de dados.

O Azure Site Recovery é Olá recomendado solução para a camada da aplicação Olá, incluindo (A) SCS. Outras aplicações, tais como aplicações SAP não NetWeaver e aplicações não SAP formam parte Olá SAP global de ambiente de implementação e também deve ser protegida com o Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Replicar máquinas virtuais
Siga [esta orientação](azure-to-azure-walkthrough-enable-replication.md) toostart replicar todos os Olá toohello de máquinas virtuais do SAP aplicação Centro de dados de DR do Azure.

Se estiver a utilizar um IP estático, pode especificar Olá IP que pretende que sejam Olá tootake de máquina virtual na secção cartões de interface de rede do Olá nas definições de rede e computação.

![IP de destino](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação
Um plano de recuperação permite a ativação pós-falha de Olá de várias camadas numa aplicação de várias camada, por conseguinte, manter a consistência da aplicação da sequência. Siga os passos de Olá descritos [aqui](site-recovery-create-recovery-plans.md) ao criar um plano de recuperação para uma aplicação web de várias camadas.

### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar scripts toohello plano de recuperação
Poderá ter toodo algumas operações em Olá ativação pós-falha de ativação pós-falha de teste de post de máquinas virtuais do Azure para a aplicações toofunction corretamente. Pode automatizar a operação de ativação pós-falha de post Olá como atualizar a entrada DNS e alterar os vínculos e ligações, adicionando scripts correspondentes no plano de recuperação Olá, conforme descrito em [neste artigo](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Atualização de DNS
Se Olá DNS está configurado para a atualização dinâmica de DNS, em seguida, as máquinas virtuais, normalmente, atualize Olá DNS com Olá novas IP assim que for iniciado. Se pretender tooadd um passo explícita de tooupdate DNS com Olá novo IPs de máquinas virtuais de Olá, adicione em seguida, isto [tooupdate IP no DNS do script](https://aka.ms/asr-dns-update) como uma ação de post em grupos de plano de recuperação.  

## <a name="example-azure-to-azure-deployment"></a>Exemplo de implementação do Azure para o Azure
Diagrama de Olá abaixo cenário de DR do Azure Site Recovery do Azure para o Azure Olá caso:
* Olá Datacenter primário está a ser Singapura (Azure Sul-Oriental) e Olá DR Centro de dados é RAE de Hong Kong (Azure Oriental).  Neste cenário, o local de elevada disponibilidade é fornecida por ter duas VMs AlwaysOn do SQL Server em execução no modo síncrono no Singapura.
* Olá ASCS de partilha de ficheiros pode ser utilizado tooprovide HA para pontos únicos de SAP Olá de falha. ASCS de partilha de ficheiros não necessita de um disco partilhado de cluster e aplicações, tais como SIOS não são necessárias.
* Proteção DR para a camada DBMS Olá é conseguida utilizando a replicação assíncrona.
* Este cenário mostra "DR simétrico" – um termo utilizado toodescribe uma solução de DR que tenha uma réplica exata de produção, por conseguinte Olá solução DR SQL Server tem elevada visibilidade local. utilização Olá DR simétrico não é obrigatória para a camada de base de dados de Olá, e muitos clientes tirar partido dos flexibilidade de Olá de implementações de nuvem toobuild um nó de disponibilidade elevada local rapidamente após um evento de DR.
* Diagrama de Olá ilustra Olá SAP NetWeaver ASCS e a camada de servidor de aplicação replicadas pelo Azure Site Recovery.

![Cenário de replicação](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Efetuar uma ativação pós-falha de teste
Siga [esta orientação](azure-to-azure-walkthrough-test-failover.md) toodo uma ativação pós-falha de teste.

1.  Aceda tooAzure portal e selecione o Cofre dos serviços de recuperação.
2.  Clique no plano de recuperação de Olá criado para aplicações SAP (s).
3.  Clique em "Ativação pós-falha de teste".
4.  Selecione o ponto de recuperação e o processo de ativação pós-falha de teste de Olá toostart rede virtual do Azure.
5.  Assim que estiver ambiente secundário Olá cópias de segurança, pode realizar as validações.
6.  Depois de validações Olá estiverem concluídas, clique em 'Limpeza ativação pós-falha de teste' e a ativação pós-falha de Olá tooclean ambiente.

## <a name="doing-a-failover"></a>Efetuar uma ativação pós-falha
Siga [esta orientação](site-recovery-failover.md) quando estão a fazer uma ativação pós-falha.

1.  Aceda tooAzure portal e selecione o Cofre dos serviços de recuperação.
2.  Clique no plano de recuperação de Olá criado para a aplicação (ões) de SAP.
3.  Clique em 'Failover'.
4.  Selecione o processo de ativação pós-falha de Olá de toostart de ponto de recuperação.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como criar uma solução de recuperação após desastre para as implementações do SAP NetWeaver utilizando o Azure Site Recovery no [deste documento técnico](http://aka.ms/asr-sap). documento Olá também descreve as recomendações para diferentes arquiteturas SAP, apresenta uma lista de aplicações suportadas e tipos VM para SAP no Azure e descreve possíveis planos de teste para a sua solução de recuperação após desastre.

Saiba mais sobre [replicar outras cargas de trabalho](site-recovery-workload.md) utilizando a recuperação de sites.
