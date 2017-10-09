---
title: "aaaAzure máquinas virtuais de elevada disponibilidade para SAP NetWeaver | Microsoft Docs"
description: Guia de elevada disponibilidade para SAP NetWeaver em Azure Virtual Machines
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Azure máquinas virtuais elevada disponibilidade para SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Máquinas virtuais do Azure é a solução de Olá para organizações que precisam de computação, armazenamento e recursos de rede, na altura mínima e sem ciclos de aprovisionamento demorado. Pode utilizar máquinas virtuais do Azure toodeploy aplicações clássico como baseado em SAP NetWeaver ABAP, Java e uma pilha ABAP + Java. Expanda a fiabilidade e disponibilidade sem recursos no local adicionais. Máquinas virtuais do Azure suporta uma conectividade entre instalações, pelo que pode integrar Virtual Machines do Azure domínios no local, nuvens privadas e horizontal do sistema SAP da sua organização.

Neste artigo, vamos abordar Olá passos que que pode tomar toodeploy sistemas SAP de elevada disponibilidade no Azure utilizando o modelo de implementação Azure Resource Manager Olá. Vamos guiá-lo estas tarefas principais:

* Localizar Olá direita guias de SAP notas e instalação listados no Olá [recursos] [ sap-ha-guide-2] secção. Este artigo complementa a documentação de instalação do SAP e notas de SAP, que são recursos primário Olá e que podem ajudar a instalar e implementar o software de SAP plataformas específicas.
* Saiba Olá diferenças e o modelo de implementação clássico do Azure de Olá do modelo de implementação Azure Resource Manager Olá.
* Saiba mais sobre os modos de quórum de Clustering de ativação pós-falha do Windows Server, pelo que pode selecionar o modelo de Olá que é mais adequado para a sua implementação do Azure.
* Saiba mais sobre o Windows Server Clustering de ativação pós-falha partilhado armazenamento nos serviços do Azure.
* Saiba como toohelp proteger único ponto de falha componentes, como o Advanced negócio Application Programming (ABAP) SAP Central serviços (ASCS) / SAP Central serviços (SCS) e sistemas de gestão de base de dados (DBMS) e os componentes redundantes como o SAP Servidor de aplicações, no Azure.
* Siga um exemplo passo a passo de uma instalação e configuração de um sistema SAP de elevada disponibilidade num cluster de Clustering de ativação pós-falha do Windows Server no Azure utilizando o Gestor de recursos do Azure.
* Saiba mais sobre toouse necessários passos adicionais Clustering de ativação pós-falha no Windows Server no Azure, mas que não são necessários numa implementação no local.

toosimplify implementação e configuração, neste artigo, utilizamos Olá modelos do Resource Manager de elevada disponibilidade de três camadas SAP. modelos de Olá automatizam a implementação de Olá toda a infraestrutura que necessita para um sistema SAP de elevada disponibilidade. infraestrutura de Olá também suporta o dimensionamento de SAP aplicação desempenho Standard (SAPS) do seu sistema SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Pré-requisitos
Antes de começar, certifique-se de que cumpre os pré-requisitos de Olá descritas Olá secções a seguir. Além disso, ser toocheck se todos os recursos listados em Olá [recursos] [ sap-ha-guide-2] secção.

Neste artigo, utilizamos modelos Azure Resource Manager para [três camadas SAP NetWeaver utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Para obter uma descrição úteis de modelos, consulte [modelos SAP Azure Resource Manager](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Recursos
Estes artigos abrangem implementações SAP no Azure:

* [Azure máquinas virtuais de planeamento e implementação de SAP NetWeaver][planning-guide]
* [Implementação de máquinas virtuais do Azure para SAP NetWeaver][deployment-guide]
* [Implementação de DBMS de máquinas virtuais do Azure para SAP NetWeaver][dbms-guide]
* [Azure máquinas virtuais elevada disponibilidade para SAP NetWeaver (deste guia)][sap-ha-guide]

> [!NOTE]
> Sempre que possível, vamos dar-lhe um toohello de ligação, consultar o guia de instalação do SAP (consulte Olá [guias de instalação do SAP][sap-installation-guides]). Pré-requisitos e informações sobre o processo de instalação de Olá, da-lo instalação de SAP NetWeaver uma boa ideia tooread Olá orienta cuidadosamente. Este artigo abrange apenas as tarefas específicas para sistemas baseados em SAP NetWeaver que pode utilizar com máquinas virtuais do Azure.
>
>

Estas notas de SAP são tópico toohello relacionados do SAP no Azure:

| Número de nota | Título |
| --- | --- |
| [1928533] |Aplicações SAP no Azure: os produtos e dimensionamento suportados |
| [2015553] |SAP no Microsoft Azure: suporta a pré-requisitos |
| [1999351] |Avançada de monitorização do Azure para SAP |
| [2178632] |Chave de monitorização métricas para SAP no Microsoft Azure |
| [1999351] |Virtualização no Windows: avançada de monitorização |
| [2243692] |Utilização do armazenamento SSD Premium do Azure para a instância do SAP DBMS |

Saiba mais sobre Olá [limitações das subscrições Azure][azure-subscription-service-limits-subscription], incluindo as limitações de predefinição geral e limitações máximas.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de elevada disponibilidade com o Azure Resource Manager vs. o modelo de implementação clássico do Azure Olá
Olá, Azure Resource Manager e modelos de implementação clássica do Azure são diferentes nos Olá seguintes áreas:

- Grupos de recursos
- Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure de Olá
- Suporte para cenários de várias SID SAP

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Grupos de recursos
No Gestor de recursos do Azure, pode utilizar toomanage de grupos de recurso todos os recursos da aplicação Olá na sua subscrição do Azure. Uma abordagem integrada, num grupo de recursos, todos os recursos ter Olá mesmo ciclo de vida. Por exemplo, todos os recursos são criados em Olá mesmo tempo e estas são eliminadas quando a Olá mesmo tempo. Saiba mais sobre [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure de Olá

No modelo de implementação clássico do Azure Olá, há uma dependência entre o Balanceador de carga interno do Azure Olá (serviço de Azure Load Balancer) e o serviço em nuvem Olá. Cada Balanceador de carga interno tem um serviço em nuvem.

No Gestor de recursos do Azure, tem de todos os recursos do Azure toobe juntar um grupo de recursos do Azure e isto é válido para o Balanceador de carga do Azure, bem como. No entanto, não há nenhum grupo de recursos do Azure toohave necessidade por Balanceador de carga do Azure, por exemplo, um grupo de recursos do Azure pode conter vários balanceadores de carga do Azure. ambiente de Olá é mais simples e mais flexíveis. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Suporte para cenários de várias SID SAP

No Gestor de recursos do Azure, pode instalar várias SAP sistema identificador (SID) ASCS/SCS instâncias de um cluster. Instâncias de várias SID são possíveis devido ao suporte para vários endereços IP para cada Balanceador de carga interno do Azure.

toouse Olá modelo de implementação clássica do Azure, siga os procedimentos de Olá descritos [SAP NetWeaver no Azure: instâncias de Clustering SAP ASCS/SCS através da utilização de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Recomendamos vivamente que utilize o modelo de implementação Azure Resource Manager Olá para as instalações de SAP. Oferece várias vantagens que não estão disponíveis no modelo de implementação clássica Olá. Saiba mais sobre o Azure [modelos de implementação][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Clustering de ativação pós-falha
Clustering de ativação pós-falha do Windows Server é foundation Olá de uma instalação de SAP ASCS/SCS de elevada disponibilidade e o DBMS no Windows.

Um cluster de ativação pós-falha é um grupo de 1 + n servidores independentes (nós) que trabalham em conjunto de disponibilidade de Olá tooincrease das aplicações e serviços. Se ocorrer uma falha de nó, Clustering de ativação pós-falha do Windows Server calcula o número de Olá de falhas que podem ocorrer, mantendo em simultâneo um bom estado de funcionamento tooprovide aplicações e serviços em cluster. Pode escolher entre diferentes quórum modos tooachieve clustering de ativação pós-falha.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Modos de quórum
Pode escolher entre quatro modos de quórum ao utilizar o Clustering de ativação pós-falha do Windows Server:

* **Maioria de nós**. Cada nó do cluster de Olá pode votar. as funções de cluster de Olá apenas com a maioria dos votos, ou seja, com mais de metade Olá votos. Recomendamos esta opção para os clusters que tem um número de nós desigual. Por exemplo, três nós num cluster de sete nós podem falhar e Olá cluster stills distribui uma maioria e continua toorun.  
* **Disco maioria de nós e**. Cada nó e um disco designado (um testemunho de disco) no armazenamento de cluster Olá podem votar quando estão disponíveis e na comunicação. as funções de cluster de Olá apenas com a maioria das Olá os votos, ou seja, com mais de metade Olá votos. Este modo faz sentido num ambiente de cluster com um número par de nós. Se nós de meio Olá e disco Olá estão online, cluster Olá permanece em bom estado.
* **Nó e o ficheiro partilham maioria**. Cada nó de adição cria uma partilha de ficheiros designado (um testemunho de partilha de ficheiros) Olá administrador pode votar, independentemente se encontram disponíveis nós Olá e partilha de ficheiros e na comunicação. as funções de cluster de Olá apenas com a maioria das Olá os votos, ou seja, com mais de metade Olá votos. Este modo faz sentido num ambiente de cluster com um número par de nós. É semelhante toohello nós e o modo de maioria de disco, mas utiliza uma partilha de ficheiros testemunha em vez de um disco testemunha. Este modo é fácil tooimplement, mas se a partilha de ficheiros de Olá propriamente dito não está altamente disponível, este poderá tornar-se um ponto único de falha.
* **Sem maioria: Disco apenas**. cluster de Olá tem um quórum se um nó estiver disponível e na comunicação com um disco específico no armazenamento de cluster Olá. Apenas Olá nós também em comunicação com esse disco podem associar cluster Olá. Recomendamos que utilize este modo.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Server Clustering de ativação pós-falha no local
Figura 1 mostra um cluster de dois nós. Se hello falha da ligação de rede entre os nós de Olá e ambos os nós permanecem cópias de segurança e em execução, uma partilha de ficheiro ou de disco de quórum determina nó que vai continuar do cluster de Olá tooprovide aplicações e serviços. nó de Olá que tem o disco de quórum do acesso toohello ou partilha de ficheiros é nó de Olá que garante que os serviços de continuam.

Uma vez que este exemplo utiliza um cluster de dois nós, utilizamos Olá nó e o modo de quórum maioria de partilha de ficheiros. Maioria de disco e Olá nó também é uma opção válida. Num ambiente de produção, recomendamos que utilize um disco de quórum. Pode utilizar o armazenamento e de rede toomake de tecnologia de sistema-altamente disponível.

![Figura 1: Exemplo de uma configuração de Clustering de ativação pós-falha do Windows Server para SAP ASCS/SCS no Azure][sap-ha-guide-figure-1000]

_**Figura 1:** exemplo de uma configuração de Clustering de ativação pós-falha do Windows Server para SAP ASCS/SCS no Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Armazenamento partilhado
Figura 1 mostra também um cluster de dois nós de armazenamento partilhado. Um cluster de armazenamento partilhado no local, todos os nós do cluster de Olá detetam armazenamento partilhado. Um mecanismo de bloqueio protege os dados de Olá contra danos. Todos os nós podem detetar se o outro nó falha. Se falhar um nó, o nó restante Olá é proprietários Olá recursos de armazenamento e garante a disponibilidade de Olá dos serviços.

> [!NOTE]
> Não precisa de discos partilhados para elevada disponibilidade com algumas aplicações DBMS, tal como com o SQL Server. SQL Server Always On replica os ficheiros de registo e dados DBMS do disco local do Olá do disco local do toohello de nó de um cluster de outro nó de cluster. Nesse caso, configuração de cluster do Windows hello não necessita de um disco partilhado.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Funcionamento em rede e resolução de nomes
Computadores cliente alcancem cluster Olá através de um endereço IP virtual e um nome de anfitrião virtual que Olá fornece de servidor DNS. Olá no local nós e servidor DNS de Olá pode processar vários endereços IP.

Uma configuração típica, utiliza dois ou mais ligações de rede:

* Armazenamento de toohello uma ligação dedicada
* Uma ligação de rede interna para o cluster para o heartbeat Olá
* Uma rede pública que os clientes utilizam tooconnect toohello cluster

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Server Clustering de ativação pós-falha no Azure
Em comparação com as implementações de nuvem privada ou metal toobare, Virtual Machines do Azure requer tooconfigure passos adicionais Clustering de ativação pós-falha do Windows Server. Quando criar um disco partilhado de cluster, terá de tooset vários endereços IP e o anfitrião virtual nomes para a instância de SAP ASCS/SCS Olá.

Neste artigo, vamos discutir conceitos chave e Olá passos adicionais necessários toobuild um cluster de elevada disponibilidade de serviços central SAP no Azure. Vamos mostrar-lhe como tooset segurança ferramenta de terceiros Olá SIOS DataKeeper e como tooconfigure Olá Azure interno Balanceador de carga. Pode utilizar estas ferramentas toocreate num cluster de ativação pós-falha do Windows com um testemunho de partilha de ficheiros no Azure.

![Figura 2: Clustering de ativação pós-falha do Windows Server configuração no Azure sem um disco partilhado][sap-ha-guide-figure-1001]

_**Figura 2:** configuração Clustering de ativação pós-falha do Windows Server no Azure sem um disco partilhado_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Partilhar o disco no Azure com SIOS DataKeeper
Precisa de cluster armazenamento partilhado para uma instância do SAP ASCS/SCS de elevada disponibilidade. Como os de Setembro de 2016, não oferta Azure armazenamento partilhado que pode utilizar toocreate um cluster de armazenamento partilhado. Pode utilizar o software de terceiros SIOS DataKeeper Cluster Edition toocreate um armazenamento espelhado que simula o armazenamento partilhado de cluster. Olá solução SIOS fornece replicação síncrona de dados em tempo real. Esta é a forma como pode criar um recurso de disco partilhado para um cluster:

1. Anexe um tooeach de disco adicional de Olá máquinas de virtuais (VMs) numa configuração de cluster do Windows.
2. Execute SIOS DataKeeper Cluster Edition em ambos os nós de máquina virtual.
3. Configure SIOS DataKeeper Cluster Edition para que este reflete o conteúdo de Olá do volume de disco adicionais ligado Olá do volume adicionais disco ligado toohello de máquina virtual de origem de Olá Olá virtual da máquina de destino. SIOS DataKeeper deduz volumes locais Olá origem e de destino e, em seguida, apresenta-los tooWindows do Clustering de ativação pós-falha como um disco partilhado.

Obter mais informações [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Figura 3: Configuração de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 3:** configuração de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper_

> [!NOTE]
> Não precisa de discos partilhados para elevada disponibilidade com alguns produtos DBMS, como o SQL Server. SQL Server Always On replica os ficheiros de registo e dados DBMS do disco local do Olá do disco local do toohello de nó de um cluster de outro nó de cluster. Neste caso, configuração de cluster do Windows hello não necessita de um disco partilhado.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Resolução de nomes no Azure
plataforma de nuvem do Azure Olá não oferece Olá opção tooconfigure endereços IP virtuais, tais como endereços IP flutuante. É necessário um tooset solução alternativa, se um virtual IP endereço tooreach Olá recurso de cluster na nuvem de Olá.
O Azure tem um balanceador de carga interno no Olá serviço de Balanceador de carga do Azure. Com o Balanceador de carga interno Olá, os clientes conseguirem contactar o cluster de Olá através de Olá cluster um endereço IP virtual.
Terá de Balanceador de carga interno Olá toodeploy no grupo de recursos de Olá que contém nós de cluster Olá. Em seguida, configure todas as portas necessárias reencaminhamento regras com sonda Olá portas Olá interno de Balanceador de carga.
os clientes de Olá podem ligar através do nome de anfitrião virtual Olá. servidor DNS Olá resolve o endereço IP de cluster Olá, porta e o Olá carga interno balanceador identificadores toohello o nó ativo do cluster de Olá de reencaminhamento.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver elevada disponibilidade no Azure infraestrutura-como-um-serviço (IaaS)
tooachieve SAP elevada de disponibilidade de aplicações, tais como para componentes de software do SAP, terá de Olá tooprotect os seguintes componentes:

* Instância de servidor de aplicações SAP
* Instância do SAP ASCS/SCS
* Servidor DBMS

Para obter mais informações sobre como proteger os componentes SAP em cenários de elevada disponibilidade, consulte [Virtual Machines do Azure de planeamento e implementação de SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Servidor de aplicações SAP de elevada disponibilidade
Normalmente, não precisa de uma solução de elevada disponibilidade específica para instâncias de servidor de aplicações SAP e a caixa de diálogo Olá. Alcançar a elevada disponibilidade através da redundância e irá configurar várias instâncias de caixa de diálogo em instâncias diferentes Virtual Machines do Azure. Deve ter, pelo menos, duas instâncias de aplicações SAP instaladas em duas instâncias de Virtual Machines do Azure.

![Figura 4: Servidor de aplicações de elevada disponibilidade SAP][sap-ha-guide-figure-2000]

_**Figura 4:** servidor de aplicações SAP de elevada disponibilidade_

Tem de colocar todas as máquinas virtuais que instâncias de servidor de aplicações SAP de anfitrião no Olá mesmo conjunto de disponibilidade do Azure. Um conjunto de disponibilidade do Azure garante que:

* Todas as máquinas virtuais fazem parte do Olá mesmo domínio de atualização. Por exemplo, um domínio de atualização, certifica-se de que Olá máquinas de virtuais não são atualizadas em Olá simultâneo durante o período de indisponibilidade de manutenção planeada.
* Todas as máquinas virtuais fazem parte do Olá mesmo domínio de falhas. Por exemplo, um domínio de falhas certifica-se de que as máquinas virtuais são implementadas para que não existe nenhum ponto único de falha afeta a disponibilidade de Olá de todas as máquinas virtuais.

Saiba mais sobre como demasiado[gerir a disponibilidade de Olá das máquinas virtuais][virtual-machines-manage-availability].

Apenas para disco não gerido: uma vez que Olá conta do storage do Azure é um potencial ponto único de falha, é importante toohave pelo menos duas contas de armazenamento do Azure, em que são distribuídas, pelo menos, duas máquinas virtuais. Uma configuração ideal, discos Olá de cada máquina virtual que está a executar uma instância de caixa de diálogo SAP seriam implementados numa conta de armazenamento diferente.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Instância do SAP ASCS/SCS de elevada disponibilidade
Figura 5 é um exemplo de uma instância do SAP ASCS/SCS de elevada disponibilidade.

![Figura 5: Instância de elevada disponibilidade SAP ASCS/SCS][sap-ha-guide-figure-2001]

_**Figura 5:** instância de elevada disponibilidade SAP ASCS/SCS_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASCS/SCS instância elevada disponibilidade com Clustering de ativação pós-falha no Windows Server no Azure
Em comparação com as implementações de nuvem privada ou metal toobare, Virtual Machines do Azure requer tooconfigure passos adicionais Clustering de ativação pós-falha do Windows Server. toobuild num cluster de ativação pós-falha do Windows, terá de um disco de cluster partilhado, vários endereços IP, vários nomes de anfitrião virtual e um balanceador de carga interno do Azure para uma instância do SAP ASCS/SCS de clustering. Vamos discutir em mais detalhe posteriormente no artigo Olá.

![Figura 6: Windows Server Clustering de ativação pós-falha para uma configuração de SAP ASCS/SCS no Azure utilizando SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 6:** Clustering de ativação pós-falha no Windows Server para uma configuração de SAP ASCS/SCS no Azure com SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Instância DBMS de elevada disponibilidade
Olá DBMS também é um único ponto de contacto num sistema SAP. Terá de tooprotect-la utilizando uma solução de elevada disponibilidade. A figura 7 mostra uma solução de elevada disponibilidade SQL Server Always On no Azure, com Clustering de ativação pós-falha do Windows Server e Olá Azure interno Balanceador de carga. SQL Server Always On replica os ficheiros de registo e dados DBMS utilizando a sua própria replicação DBMS. Neste caso, a não precisa de discos de cluster partilhados, que simplifica a configuração completa Olá.

![A figura 7: Exemplo de um DBMS de SAP de elevada disponibilidade, com o SQL Server Always On][sap-ha-guide-figure-2003]

_**A figura 7:** exemplo de um DBMS de SAP de elevada disponibilidade, com o SQL Server Always On_

Para obter mais informações sobre o clustering do SQL Server no Azure utilizando o modelo de implementação Azure Resource Manager Olá, consulte estes artigos:

* [Configurar o grupo de disponibilidade Always On em Azure Virtual Machines manualmente utilizando o Gestor de recursos] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Configurar um balanceador de carga interno do Azure para um grupo de disponibilidade Always On no Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Cenários de implementação de elevada disponibilidade de ponto a ponto

### <a name="deployment-scenario-using-architectural-template-1"></a>Cenário de implementação através da arquitetura de modelo de 1

Figura 8 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP. Este cenário é configure da seguinte forma:

- Um cluster dedicado é utilizado para a instância de SAP ASCS/SCS Olá.
- Um cluster dedicado é utilizado para a instância DBMS Olá.
- Instâncias de servidor de aplicações SAP são implementadas na suas própria VMs dedicadas.

![Figura 8: SAP elevada disponibilidade da arquitetura modelo 1, com o cluster dedicado para ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

_**Figura 8:** SAP 1 modelo da arquitetura do elevada disponibilidade, clusters dedicados para ASCS/SCS e DBMS_

### <a name="deployment-scenario-using-architectural-template-2"></a>Cenário de implementação através da arquitetura de modelo de 2

A figura 9 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP. Este cenário é configure da seguinte forma:

- Um cluster dedicado é utilizado para **ambos** Olá SAP ASCS/SCS instância e Olá DBMS.
- Instâncias de servidor de aplicações SAP são implementadas na próprias VMs dedicadas.

![Figura 9: SAP elevada disponibilidade da arquitetura modelo 2, com um cluster dedicado para ASCS/SCS e um cluster dedicado para DBMS][sap-ha-guide-figure-2005]

_**Figura 9:** SAP elevada disponibilidade da arquitetura modelo 2, com um cluster dedicado para ASCS/SCS e um cluster dedicado para DBMS_

### <a name="deployment-scenario-using-architectural-template-3"></a>Cenário de implementação através da arquitetura de modelo de 3

A figura 10 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **dois** SAP sistemas, com &lt;SID1&gt; e &lt;SID2&gt;. Este cenário é configure da seguinte forma:

- Um cluster dedicado é utilizado para **ambos** instância Olá SAP ASCS/SCS SID1 *e* instância Olá SAP ASCS/SCS SID2 (um cluster).
- Um cluster dedicado é utilizado para DBMS SID1 e outro cluster dedicado é utilizado para DBMS SID2 (dois clusters).
- As instâncias de servidor de aplicações do SAP para Olá sistema SAP SID1 ter os seus próprios VMs dedicadas.
- As instâncias de servidor de aplicações do SAP para Olá sistema SAP SID2 ter os seus próprios VMs dedicadas.

![Figura 10: SAP elevada disponibilidade da arquitetura modelo 3, com um cluster dedicado para instâncias ASCS/SCS diferentes][sap-ha-guide-figure-6003]

_**Figura 10:** SAP elevada disponibilidade da arquitetura modelo 3, com um cluster dedicado para instâncias ASCS/SCS diferentes_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar a infraestrutura de Olá

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Preparar a infraestrutura de Olá da arquitetura de modelo de 1
Modelos Azure Resource Manager para SAP ajudam a simplificar a implementação dos recursos necessários.

modelos de três camadas Olá no Gestor de recursos do Azure também suportam cenários de elevada disponibilidade, tal como 1 da arquitetura do modelo, que tem dois clusters. Cada cluster é um ponto de falha para SAP ASCS/SCS e DBMS SAP único.

Aqui é onde pode obter os modelos Azure Resource Manager para o cenário de exemplo de Olá que dita neste artigo:

* [Imagem do Marketplace do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Imagem do Marketplace do Azure utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Imagem personalizada utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

infraestrutura de Olá tooprepare para 1 da arquitetura do modelo:

- No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **SYSTEMAVAILABILITY** caixa, selecione **HA**.

  ![Figura 11: Definir os parâmetros do SAP elevada disponibilidade do Azure Resource Manager][sap-ha-guide-figure-3000]

_**Figura 11:** definir os parâmetros do SAP elevada disponibilidade do Azure Resource Manager_


  criam modelos de Olá:

  * **Máquinas virtuais**:
    * Máquinas de virtuais do servidor de aplicações SAP: <*SAPSystemSID*> - di - <*número*>
    * Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*> - ascs - <*número*>
    * DBMS cluster: <*SAPSystemSID*> - db - <*número*>

  * **Rede de cartões de todas as máquinas virtuais, com os endereços IP associados**:
    * <*SAPSystemSID*> - nic - di - <*número*>
    * <*SAPSystemSID*> - nic - ascs - <*número*>
    * <*SAPSystemSID*> - nic - db - <*número*>

  * **Contas de armazenamento do Azure (apenas discos não geridos)**

  * **Grupos de disponibilidade** para:
    * Máquinas de virtuais do servidor de aplicações SAP: <*SAPSystemSID*> - avset - di
    * Máquinas virtuais de cluster do SAP ASCS/SCS: <*SAPSystemSID*> - avset - ascs
    * Máquinas virtuais de cluster DBMS: <*SAPSystemSID*> - avset - db

  * **Balanceador de carga interno do Azure**:
    * Com todas as portas para a instância ASCS/SCS Olá e endereço IP <*SAPSystemSID*> - lb - ascs
    * Com todas as portas para o endereço IP e o SQL Server DBMS Olá <*SAPSystemSID*> - lb - db

  * **Grupo de segurança de rede**: <*SAPSystemSID*> - nsg - ascs-0  
    * Com um abra toohello de porta de protocolo RDP (Remote Desktop Protocol) externo <*SAPSystemSID*> - ascs - 0 máquina

> [!NOTE]
> Todos os endereços IP de placas de rede Olá e Balanceadores de carga internos do Azure são **dinâmica** por predefinição. Alterá-los demasiado**estático** endereços IP. Vamos descrever como toodo este artigo Olá.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implementar máquinas virtuais com toouse de conectividade (em vários locais) da rede empresarial na produção
Para sistemas de produção SAP, implementar máquinas virtuais do Azure com [conectividade de rede empresarial (em vários locais)] [ planning-guide-2.2] através da utilização do Azure Site a Site VPN ou Azure ExpressRoute.

> [!NOTE]
> Pode utilizar a instância de rede Virtual do Azure. rede virtual Olá e sub-rede já tiverem sido criados e preparados.
>
>

1.  No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **NEWOREXISTINGSUBNET** caixa, selecione **existente**.
2.  No Olá **SUBNETID** caixa, adicione a cadeia completa de Olá da sua rede de Azure preparado SubnetID onde planeia toodeploy as máquinas virtuais do Azure.
3.  tooget uma lista de todas as sub-redes de rede do Azure, execute este comando do PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Olá **ID** campo mostra Olá **SUBNETID**.
4. tooget uma lista de todos os **SUBNETID** valores, execute este comando do PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Olá **SUBNETID** se parece com isto:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Implementar instâncias SAP apenas na nuvem para teste e demonstração
Pode implementar o sistema SAP de elevada disponibilidade de um modelo de implementação apenas de nuvem. Este tipo de implementação é principalmente útil para casos de utilização de demonstração e teste. Não é adequada para os casos de utilização de produção.

- No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **NEWOREXISTINGSUBNET** caixa, selecione **novo**. Deixe Olá **SUBNETID** campo vazio.

  Olá SAP do Azure Resource Manager modelo cria automaticamente Olá rede virtual do Azure e a sub-rede.

> [!NOTE]
> Também precisa de toodeploy pelo menos um dedicado a máquina virtual para o Active Directory e DNS no Olá a mesma instância de rede Virtual do Azure. modelo de Olá não crie estas máquinas virtuais.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Preparar a infraestrutura de Olá da arquitetura de modelo de 2

Pode utilizar este modelo Azure Resource Manager para SAP toohelp simplificar a implementação de recursos de infraestrutura necessária para SAP da arquitetura modelo 2.

Aqui é onde pode obter os modelos Azure Resource Manager para este cenário de implementação:

* [Imagem do Marketplace do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Imagem do Marketplace do Azure utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Imagem personalizada utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Preparar a infraestrutura de Olá da arquitetura de modelo de 3

Pode preparar infraestrutura Olá e configurar o SAP para **várias SID**. Por exemplo, pode adicionar uma instância adicional do SAP ASCS/SCS para um *existente* configuração de cluster. Para obter mais informações, consulte [configurar uma instância adicional do SAP ASCS/SCS para um toocreate de configuração de cluster existentes uma configuração de várias SID SAP no Gestor de recursos do Azure][sap-ha-multi-sid-guide].

Se quiser toocreate um novo cluster de múltiplos SID, pode utilizar Olá várias-SID [modelos de início rápido no GitHub](https://github.com/Azure/azure-quickstart-templates).
um novo cluster de múltiplos SID toocreate, terá de Olá toodeploy seguintes três modelos:

* [Modelo ASCS/SCS](#ASCS-SCS-template)
* [Modelo de base de dados](#database-template)
* [Modelo de servidores de aplicações](#application-servers-template)

Olá secções seguintes tem mais detalhes sobre os modelos de Olá e parâmetros de Olá terá tooprovide nos modelos de Olá.

#### <a name="ASCS-SCS-template"></a>Modelo ASCS/SCS

modelo ASCS/SCS Olá implementa duas máquinas virtuais que pode utilizar toocreate um cluster de ativação pós-falha do Windows Server que aloja várias instâncias ASCS/SCS.

tooset segurança modelo Olá ASCS/SCS várias-SID, Olá [modelo de várias SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] ou [modelo de várias SID ASCS/SCS utilizando discos geridos] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:

  - **Prefixo de recurso**.  Defina o prefixo de recurso Olá, o que é utilizado tooprefix todos os recursos que são criados durante a implementação de Olá. Porque os recursos de Olá não pertencer um sistema SAP tooonly, prefixo Olá do recurso de Olá não é Olá SID de um sistema SAP.  prefixo de Olá tem de estar entre **três e seis carateres**.
  - **Tipo de pilha**. Selecione o tipo de pilha de Olá de Olá sistema SAP. Dependendo do tipo de pilha Olá, o Balanceador de carga do Azure tem um (ABAP ou apenas Java) ou dois (ABAP + Java) endereços IP privados por sistema SAP.
  -  **Tipo de SO**. Selecione o sistema de operativo Olá das máquinas de virtuais Olá.
  -  **Contagem de sistema do SAP**. Selecione o número de Olá dos sistemas SAP pretende tooinstall neste cluster.
  -  **Disponibilidade do sistema**. Selecione **HA**.
  -  **Nome de utilizador de administrador e a palavra-passe de administrador**. Crie um novo utilizador que pode ser utilizado toosign toohello máquina.
  -  **Novo ou existente sub-rede**. Defina se um nova rede virtual e a sub-rede devem ser criados ou, deve ser utilizada uma sub-rede existente. Se já tiver uma rede virtual que é a rede no local de tooyour ligado, selecione **existente**.
  -  **Id de sub-rede**. Definir o ID de Olá de Olá toowhich sub-rede de Olá devem estar ligadas a máquinas virtuais. Selecione a sub-rede de Olá da sua rede privada virtual (VPN) ou ExpressRoute rede virtual tooconnect Olá tooyour no local rede da máquina virtual. ID de Olá, normalmente, este aspeto:

   /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} <*id de subscrição*> /resourceGroups/ <*nome do grupo de recursos*> /providers/Microsoft.Network/virtualNetworks/ <*nome da rede virtual*> /subnets/ <*nome de sub-rede*>

modelo de Olá implementa uma instância de Balanceador de carga do Azure, que suporta vários sistemas SAP.

- instâncias ASCS Olá estão configuradas para o número da instância 00, 10, 20...
- instâncias SCS Olá estão configuradas para o número da instância 01, 11, 21...
- instâncias de servidor de replicação de colocar em fila do ASCS (ERS) (apenas Linux) Olá estão configuradas para o número da instância 02, 12, 22...
- instâncias do Olá SCS ERS (apenas Linux) estão configuradas para o número da instância 03, 13, 23...

Olá Balanceador de carga contém 1 (2 para Linux) VIP(s), 1 x VIP para ASCS/SCS e 1 x VIP para ERS (apenas Linux).

Olá lista seguinte contém todas as regras de (em que x é o número de Olá de Olá sistema SAP, por exemplo, 1, 2, 3...) de balanceamento de carga:
- Portas específicas do Windows para cada sistema SAP: 445, 5985
- Portas ASCS (número de instância x0): 32 x 0, 36 x 0, -39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016
- Portas SCS (número de instância x1): 32 x 1 33 x 1, 39 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116
- ASCS ERS portas no Linux (número de instância x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216
- SCS ERS portas no Linux (número de instância x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316

Balanceador de carga Olá é Olá toouse configurado portas de pesquisa (em que x é o número de Olá de Olá sistema SAP, por exemplo, 1, 2,... 3) os seguintes:
- Porta de sonda do Balanceador de carga internos ASCS/SCS: 620 x 0
- Porta da sonda (apenas Linux) do Balanceador de carga ERS internos: 621 x 2

#### <a name="database-template"></a>Modelo de base de dados

modelo de base de dados de Olá implementa uma ou duas máquinas virtuais que pode utilizar tooinstall Olá sistema de gestão de base de dados relacional (RDBMS) para um sistema SAP. Por exemplo, se implementar um modelo ASCS/SCS para sistemas SAP cinco, terá de toodeploy este modelo de cinco vezes.

tooset segurança Olá da base de dados várias SID modelo, Olá [modelo várias SID de base de dados] [ sap-templates-3-tier-multisid-db-marketplace-image] ou [modelo de várias SID de base de dados utilizando discos geridos] [ sap-templates-3-tier-multisid-db-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:

  -  **Id de sistema de SAP**. Introduza o ID de sistema SAP Olá de Olá sistema SAP pretende tooinstall. Olá ID será utilizado como um prefixo para recursos de Olá que são implementados.
  -  **Tipo de SO**. Selecione o sistema de operativo Olá das máquinas de virtuais Olá.
  -  **DbType**. Selecione o tipo de Olá da base de dados de Olá pretende tooinstall no cluster de Olá. Selecione **SQL** se quiser tooinstall Microsoft SQL Server. Selecione **HANA** se máquinas de virtuais Olá planeia tooinstall SAP HANA. Certifique-se tooselect Olá tipo de sistema operativo correto: selecione **Windows** para SQL Server, selecione uma distribuição Linux para HANA. Olá Balanceador de carga do Azure que está ligado toohello máquinas virtuais estejam configuradas tipo de base de dados do toosupport Olá selecionado:
    * **SQL SERVER**. Balanceador de carga Olá será a porta 1433 balanceamento de carga. Certifique-se de que toouse esta porta para a configuração do SQL Server Always On.
    * **HANA**. Balanceador de carga Olá serão as portas 35015 e 35017 de balanceamento de carga. Certifique-se de que tooinstall SAP HANA com o número de instância **50**.
    Balanceador de carga Olá utilizará a porta da sonda 62550.
  -  **Tamanho do sistema de SAP**. Número de Olá conjunto de novo sistema do SAPS Olá irá fornecer. Se tiver a não certeza necessitará de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.
  -  **Disponibilidade do sistema**. Selecione **HA**.
  -  **Nome de utilizador de administrador e a palavra-passe de administrador**. Crie um novo utilizador que pode ser utilizado toosign toohello máquina.
  -  **Id de sub-rede**. Introduza o ID de Olá da sub-rede Olá que utilizou durante a implementação de Olá do modelo ASCS/SCS hello, ou Olá ID de sub-rede de Olá que foi criada como parte da implementação do modelo ASCS/SCS de Olá.

#### <a name="application-servers-template"></a>Modelo de servidores de aplicações

modelo de servidores de aplicação Olá implementa dois ou mais máquinas virtuais que podem ser utilizadas como instâncias de servidor de aplicações do SAP para um sistema SAP. Por exemplo, se implementar um modelo ASCS/SCS para sistemas SAP cinco, terá de toodeploy este modelo de cinco vezes.

tooset segurança Olá servidores múltiplos SID modelo de aplicação, na Olá [modelo de SID de múltiplos servidores de aplicações] [ sap-templates-3-tier-multisid-apps-marketplace-image] ou [modelo SID de múltiplos servidores de aplicações utilizando discos geridos] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:

  -  **Id de sistema de SAP**. Introduza o ID de sistema SAP Olá de Olá sistema SAP pretende tooinstall. Olá ID será utilizado como um prefixo para recursos de Olá que são implementados.
  -  **Tipo de SO**. Selecione o sistema de operativo Olá das máquinas de virtuais Olá.
  -  **Tamanho do sistema de SAP**. número de Olá de novo sistema do SAPS Olá irá fornecer. Se tiver a não certeza necessitará de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.
  -  **Disponibilidade do sistema**. Selecione **HA**.
  -  **Nome de utilizador de administrador e a palavra-passe de administrador**. Crie um novo utilizador que pode ser utilizado toosign toohello máquina.
  -  **Id de sub-rede**. Introduza o ID de Olá da sub-rede Olá que utilizou durante a implementação de Olá do modelo ASCS/SCS hello, ou Olá ID de sub-rede de Olá que foi criada como parte da implementação do modelo ASCS/SCS de Olá.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Rede virtual do Azure
No nosso exemplo, o espaço de endereços de Olá de Olá rede virtual do Azure é 10.0.0.0/16. Há uma sub-rede denominada **sub-rede**, com um intervalo de endereços de 10.0.0.0/24. Todos os balanceadores de carga internos e máquinas virtuais são implementados nesta rede virtual.

> [!IMPORTANT]
> Não efetue as alterações toohello as definições de rede dentro Olá sistema operativo. Isto inclui os endereços IP, servidores DNS e sub-rede. Configure as definições de rede no Azure. serviço de protocolo de configuração dinâmica de anfitrião (DHCP) de Olá propaga as suas definições.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Endereços IP de DNS

Olá tooset necessário que endereços IP de DNS, Olá os seguintes passos.

1.  No Olá portal do Azure, no Olá **servidores DNS** painel, certifique-se de que a rede virtual **servidores DNS** opção estiver definida demasiado**DNS personalizado**.
2.  Selecione as definições com base no tipo de Olá de rede que tiver. Para obter mais informações, consulte Olá os seguintes recursos:
    * [Conectividade de rede empresarial (em vários locais)][planning-guide-2.2]: adicionar endereços IP Olá dos servidores DNS Olá no local.  
    Pode expandir no local DNS servidores toohello máquinas virtuais que estão em execução no Azure. Nesse cenário, pode adicionar endereços IP Olá de Olá Azure máquinas virtuais em que executa o serviço DNS Olá.
    * [Implementação apenas de nuvem][planning-guide-2.1]: implementar uma máquina virtual adicional no Olá mesma instância de rede Virtual que funciona como um servidor DNS. Adicionar endereços de IP Olá Olá Azure máquinas virtuais que configurou toorun serviço DNS.

    ![Figura 12: Configure os servidores DNS para a rede Virtual do Azure][sap-ha-guide-figure-3001]

    _**Figura 12:** configurar DNS servidores para a rede Virtual do Azure_

  > [!NOTE]
  > Se alterar os endereços IP Olá dos servidores DNS Olá, terá de toorestart Olá máquinas virtuais do Azure tooapply Olá alteração e novos servidores DNS Olá de propagação.
  >
  >

No nosso exemplo Olá serviço DNS é instalado e configurado nestas máquinas virtuais do Windows:

| Função de máquina virtual | Nome de anfitrião de máquina virtual | Nome da placa de rede | Endereço IP estático |
| --- | --- | --- | --- |
| Primeiro servidor de DNS |domcontr-0 |PR1-nic-domcontr-0 |10.0.0.10 |
| Segundo servidor DNS |domcontr-1 |PR1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nomes de anfitriões e endereços IP estáticos para a instância em cluster do SAP ASCS/SCS Olá e instância em cluster DBMS

Para implementação no local, terá destes nomes de anfitrião reservado e endereços IP:

| Função de nome de anfitrião virtual | Nome de anfitrião virtual | Endereço IP estático virtual |
| --- | --- | --- |
| SAP ASCS/SCS primeiro cluster nome de anfitrião virtual (para gestão de cluster) |PR1-ascs-vir |10.0.0.42 |
| Nome de anfitrião virtual de instância do SAP ASCS/SCS |PR1-ascs-sap |10.0.0.43 |
| Nome de anfitrião virtual de cluster segundo do SAP DBMS (gestão de clusters) |PR1-dbms-vir |10.0.0.32 |

Quando criar o cluster de Olá, criar Olá nomes de anfitrião virtual **pr1-ascs-vir** e **pr1-dbms-vir** e Olá associadas a endereços IP que gerir Olá cluster em si. Para obter informações sobre como toodo esta, consulte [recolher nós de cluster numa configuração de cluster][sap-ha-guide-8.12.1].

Pode criar manualmente Olá outros dois nomes de anfitrião virtual, **pr1-ascs-sap** e **pr1-dbms-sap**, e Olá associadas a endereços IP, no servidor DNS Olá. Olá instância em cluster do SAP ASCS/SCS e Olá em cluster DBMS instância utilizar estes recursos. Para obter informações sobre como toodo esta, consulte [criar um nome de anfitrião virtual para uma instância em cluster do SAP ASCS/SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de endereços IP estáticos para SAP Olá máquinas virtuais
Depois de implementar Olá toouse de máquinas virtuais do cluster, terá de endereços IP estáticos do tooset todas as máquinas virtuais. Opte por fazê-lo na configuração de rede Virtual do Azure Olá e não no sistema de operativo convidado Olá.

1.  No portal do Azure Olá, selecione **grupo de recursos** > **placa de rede** > **definições** > **endereço IP** .
2.  No Olá **endereços IP** painel, em **atribuição**, selecione **estático**. No Olá **endereço IP** box, introduza o endereço IP Olá que pretende que o toouse.

  > [!NOTE]
  > Se alterar o endereço IP Olá de placa de rede Olá, terá de toorestart Olá máquinas virtuais do Azure tooapply Olá alteração.  
  >
  >

  ![Figura 13: Conjunto de endereços IP estáticos para a placa de rede Olá de cada máquina virtual][sap-ha-guide-figure-3002]

  _**Figura 13:** conjunto de endereços IP estáticos para a placa de rede Olá de cada máquina virtual_

  Repita este passo para todas as interfaces de rede, ou seja, todas as máquinas virtuais, incluindo máquinas virtuais que pretende que toouse para o seu serviço DNS/do Active Directory.

No nosso exemplo, temos destas máquinas virtuais e endereços IP estáticos:

| Função de máquina virtual | Nome de anfitrião de máquina virtual | Nome da placa de rede | Endereço IP estático |
| --- | --- | --- | --- |
| Primeira instância de servidor de aplicações SAP |PR1-di-0 |PR1-nic-di-0 |10.0.0.50 |
| Segunda instância de servidor de aplicações SAP |PR1-di-1 |PR1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Última instância do servidor de aplicações SAP |PR1-di-5 |PR1-nic-di-5 |10.0.0.55 |
| Primeiro nó de cluster para a instância ASCS/SCS |PR1-ascs-0 |PR1-nic-ascs-0 |10.0.0.40 |
| Segundo nó de cluster para a instância ASCS/SCS |PR1-ascs-1 |PR1-nic-ascs-1 |10.0.0.41 |
| Primeiro nó de cluster para a instância DBMS |PR1-db-0 |PR1-nic-db-0 |10.0.0.30 |
| Segundo nó de cluster para a instância DBMS |PR1-db-1 |PR1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Definir um endereço IP estático para o Balanceador de carga interno do Azure Olá

modelo de SAP Azure Resource Manager Olá cria um balanceador de carga interno do Azure que é utilizado para o cluster de instância do SAP ASCS/SCS Olá e cluster DBMS Olá.

> [!IMPORTANT]
> Olá endereço IP do nome de anfitrião virtual Olá de Olá SAP ASCS/SCS é Olá mesmo como endereço IP Olá Olá Balanceador de carga interno SAP ASCS/SCS: **pr1-lb-ascs**.
> Olá endereço IP do nome virtual Olá Olá DBMS é Olá mesmo como endereço IP Olá Olá Balanceador de carga interno DBMS: **pr1-lb-dbms**.
>
>

Balanceador de carga tooset um endereço IP estático para Olá Azure interno:

1.  Olá implementação inicial define o endereço IP de Balanceador de carga interno Olá demasiado**dinâmica**. No Olá portal do Azure, no Olá **endereços IP** painel, em **atribuição**, selecione **estático**.
2.  Definir o endereço IP de Olá do Balanceador de carga interno Olá **pr1-lb-ascs** toohello o endereço IP do nome de anfitrião virtual Olá da instância de SAP ASCS/SCS Olá.
3.  Definir o endereço IP de Olá do Balanceador de carga interno Olá **pr1-lb-dbms** toohello o endereço IP do nome de anfitrião virtual Olá da instância DBMS Olá.

  ![Figura 14: Conjunto de endereços IP estáticos para o Balanceador de carga interno Olá para a instância de SAP ASCS/SCS Olá][sap-ha-guide-figure-3003]

  _**Figura 14:** conjunto de endereços IP estáticos para o Balanceador de carga interno Olá para a instância de SAP ASCS/SCS Olá_

No nosso exemplo, temos de dois balanceadores de carga internos do Azure que tenham estes endereços IP estáticos:

| Função do Balanceador de carga interno do Azure | Nome do Balanceador de carga interno do Azure | Endereço IP estático |
| --- | --- | --- |
| Balanceador de carga interno de instância do SAP ASCS/SCS |PR1-lb-ascs |10.0.0.43 |
| Balanceador de carga interno SAP DBMS |PR1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga na ASCS/SCS predefinido

modelo de SAP Azure Resource Manager Olá cria portas Olá que precisa de:
* Uma instância de ABAP ASCS, com o número de instância predefinido Olá **00**
* Uma instância de Java SCS, com o número de instância predefinido Olá **01**

Quando instalar a instância do SAP ASCS/SCS, tem de utilizar o número de instância predefinido Olá **00** para sua ABAP ASCS instância e Olá instância número predefinido **01** para a instância do SCS de Java.

Em seguida, crie necessária pontos finais relativas às portas de SAP NetWeaver Olá de balanceamento de carga interna.

toocreate necessários pontos finais de balanceamento de carga interno, primeiro, crie estes pontos finais relativas às portas de SAP NetWeaver ABAP ASCS Olá de balanceamento de carga:

| Nome de regra de balanceamento de carga do serviço | Números de porta predefinidos | Portas concretas para (instância ASCS com o número de instância 00) (ERS com 10) |
| --- | --- | --- |
| Servidor de colocar em fila / *lbrule3200* |32 <*InstanceNumber*> |3200 |
| Servidor de mensagens ABAP / *lbrule3600* |36 <*InstanceNumber*> |3600 |
| Mensagem ABAP interna / *lbrule3900* |39 <*InstanceNumber*> |3900 |
| Mensagens HTTP do servidor / *Lbrule8100* |81 <*InstanceNumber*> |8100 |
| SAP iniciar serviço ASCS HTTP / *Lbrule50013* |5 <*InstanceNumber*> 13 |50013 |
| SAP iniciar serviço ASCS HTTPS / *Lbrule50014* |5 <*InstanceNumber*> 14 |50014 |
| Replicação de colocar em fila / *Lbrule50016* |5 <*InstanceNumber*> 16 |50016 |
| HTTP de ERS de serviço de início SAP *Lbrule51013* |5 <*InstanceNumber*> 13 |51013 |
| HTTP de ERS de serviço de início SAP *Lbrule51014* |5 <*InstanceNumber*> 14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| Partilha de ficheiros *Lbrule445* | |445 |

_**Tabela 1:** porta número de instâncias de SAP NetWeaver ABAP ASCS Olá_

Em seguida, crie estes pontos finais relativas às portas de SAP NetWeaver Java SCS Olá de balanceamento de carga:

| Nome de regra de balanceamento de carga do serviço | Números de porta predefinidos | Portas concretas para (instância SCS com o número de instância 01) (ERS com 11) |
| --- | --- | --- |
| Servidor de colocar em fila / *lbrule3201* |32 <*InstanceNumber*> |3201 |
| Servidor de gateway / *lbrule3301* |33 <*InstanceNumber*> |3301 |
| Servidor de mensagens de Java / *lbrule3900* |39 <*InstanceNumber*> |3901 |
| Mensagens HTTP do servidor / *Lbrule8101* |81 <*InstanceNumber*> |8101 |
| SAP iniciar serviço SCS HTTP / *Lbrule50113* |5 <*InstanceNumber*> 13 |50113 |
| SAP iniciar serviço SCS HTTPS / *Lbrule50114* |5 <*InstanceNumber*> 14 |50114 |
| Replicação de colocar em fila / *Lbrule50116* |5 <*InstanceNumber*> 16 |50116 |
| HTTP de ERS de serviço de início SAP *Lbrule51113* |5 <*InstanceNumber*> 13 |51113 |
| HTTP de ERS de serviço de início SAP *Lbrule51114* |5 <*InstanceNumber*> 14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| Partilha de ficheiros *Lbrule445* | |445 |

_**Tabela 2:** porta número de instâncias de SAP NetWeaver Java SCS Olá_

![Figura 15: Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga na predefinição ASCS/SCS][sap-ha-guide-figure-3004]

_**Figura 15:** regras para o Balanceador de carga interno do Azure Olá de balanceamento de carga de predefinição ASCS/SCS_

Definir o endereço IP Olá Olá de Balanceador de carga **pr1-lb-dbms** toohello o endereço IP do nome de anfitrião virtual Olá da instância DBMS Olá.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Altere as regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do Olá ASCS/SCS predefinido

Se quiser toouse diferentes números de Olá SAP ASCS ou instâncias SCS, tem de alterar os nomes de Olá e valores das suas portas de valores predefinidos.

1.  No portal do Azure Olá, selecione  **<* SID*> - lb - ascs carregar balanceador * * > **regras de balanceamento de carga**.
2.  Todas as regras que pertencem toohello SAP ASCS ou uma instância de SCS de balanceamento de carga, altere estes valores:

  * Nome
  * Porta
  * Porta de back-end

  Por exemplo, se pretender que o número de instância do toochange Olá predefinido ASCS de 00 too31, terá das alterações de Olá toomake para todas as portas listadas na tabela 1.

  Eis um exemplo de uma atualização para a porta *lbrule3200*.

  ![Figura 16: Alterar as regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do Olá ASCS/SCS predefinido][sap-ha-guide-figure-3005]

  _**Figura 16:** alteração Olá ASCS/SCS predefinido balanceamento de carga regras Olá Azure interno Balanceador de carga_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Adicionar o domínio de toohello de máquinas virtuais do Windows

Depois de atribuir um endereço IP estático máquinas de virtuais de toohello, adicione domínio de toohello Olá máquinas virtuais.

![Figura 17: Adicionar um domínio de tooa de máquina virtual][sap-ha-guide-figure-3006]

_**Figura 17:** adicionar um domínio de tooa de máquina virtual_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Adicionar entradas de registo em ambos os nós de cluster de instância de SAP ASCS/SCS Olá

Balanceador de carga do Azure tem um balanceador de carga interno que fechar ligações quando ligações Olá estão Inativas, defina durante um período de tempo (um tempo limite de inatividade). Os processos de trabalho do SAP na caixa de diálogo instâncias abrir ligações toohello SAP colocar em fila processam assim Olá primeiro colocar em fila/anular pedido toobe necessidades, enviada. Estas ligações normalmente permanecem estabelecidas até que o processo de trabalho de Olá ou Olá colocar em fila processo reinicia. No entanto, se Olá estiver inativa durante um período de tempo definido, Olá ligações de Olá de fechar de Balanceador de carga interno do Azure. Esta operação não é um problema porque Olá processo de trabalho SAP reestablishes o processo de colocar em fila Olá ligação toohello se já não existe. Estas atividades estão documentadas em rastreios de programador Olá dos processos SAP, mas que crie uma grande quantidade de conteúdo adicional nesses rastreios. É Olá de toochange uma boa ideia TCP/IP `KeepAliveTime` e `KeepAliveInterval` em ambos os nós de cluster. Combine estas alterações nos parâmetros de TCP/IP Olá com parâmetros de perfil do SAP, descritos mais à frente artigo Olá.

entradas do registo tooadd em ambos os nós de cluster de instância do SAP ASCS/SCS Olá, primeiro, adicione estas entradas de registo do Windows em ambos os nós de cluster do Windows para SAP ASCS/SCS:

| Caminho | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome da variável |`KeepAliveTime` |
| Tipo de variável |REG_DWORD (Decimal) |
| Valor |120000 |
| Ligação toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabela 3:** alteração Olá primeiro TCP/IP parâmetro_

Em seguida, adicione este entradas de registo do Windows em ambos os nós de cluster do Windows para SAP ASCS/SCS:

| Caminho | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome da variável |`KeepAliveInterval` |
| Tipo de variável |REG_DWORD (Decimal) |
| Valor |120000 |
| Ligação toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabela 4:** alteração Olá segundo TCP/IP parâmetro_

**alterações de Olá tooapply, reinicie ambos os nós de cluster**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Configurar um cluster de Clustering de ativação pós-falha do Windows Server para uma instância do SAP ASCS/SCS

Configurar um cluster de Clustering de ativação pós-falha do Windows Server para uma instância do SAP ASCS/SCS envolve estas tarefas:

- Recolha de nós de cluster Olá numa configuração de cluster
- Configurar um testemunho de partilha de ficheiros do cluster

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Recolher nós de cluster Olá numa configuração de cluster

1.  Olá adicionar funções e funcionalidades do assistente, adicione tooboth nós de cluster de clustering de ativação pós-falha.
2.  Configure o cluster de ativação pós-falha de Olá utilizando o Gestor de clusters de ativação pós-falha. No Gestor de clusters de ativação pós-falha, selecione **criar Cluster**e, em seguida, adicione apenas Olá nome de cluster de primeiro Olá, a nó. Não adicionar o Olá segundo nó ainda; irá adicionar o segundo nó de Olá num passo posterior.

  ![Figura 18: Adicionar servidor Olá ou nome de máquina virtual do nó do cluster primeiro Olá][sap-ha-guide-figure-3007]

  _**Figura 18:** adicionar Olá servidor ou máquina virtual o nome do nó do cluster primeiro Olá_

3.  Introduza o nome de rede Olá (nome de anfitrião virtual) do cluster de Olá.

  ![Figura 19: Introduza o nome do cluster Olá][sap-ha-guide-figure-3008]

  _**Figura 19:** introduza o nome de cluster Olá_

4.  Depois de criar o cluster de Olá, execute um teste de validação de cluster.

  ![Figura 20: Executar a verificação de validação de cluster de Olá][sap-ha-guide-figure-3009]

  _**Figura 20:** executar verificação de validação de cluster Olá_

  Pode ignorar quaisquer avisos sobre discos neste momento no processo de Olá. Irá adicionar que um testemunho de partilha de ficheiros e Olá SIOS discos partilhados mais tarde. Nesta fase, não precisa de tooworry relacionada com um quórum.

  ![Figura 21: For encontrado nenhum disco de quórum][sap-ha-guide-figure-3010]

  _**Figura 21:** não for encontrado nenhum disco de quórum_

  ![Figura 22: Recurso de cluster Core necessita de um novo endereço IP][sap-ha-guide-figure-3011]

  _**Figura 22:** recurso de cluster Core necessita de um novo endereço IP_

5.  Alterar o endereço IP Olá Olá principal de serviço de cluster. cluster de Olá não é possível iniciar até alterar o endereço IP Olá Olá principal de serviço de cluster, porque o endereço IP de hello do servidor de Olá pontos tooone de nós de máquina virtual de Olá. Fazê-lo no Olá **propriedades** página do recurso de IP do serviço de Olá core cluster.

  Por exemplo, é necessário um endereço IP de tooassign (no nosso exemplo, **10.0.0.42**) para o nome de anfitrião virtual de cluster Olá **pr1-ascs-vir**.

  ![Figura 23: Na caixa de diálogo de propriedades de Olá, alterar o endereço IP Olá][sap-ha-guide-figure-3012]

  _**Figura 23:** no Olá **propriedades** caixa de diálogo, o endereço IP de Olá de alteração_

  ![Figura 24: Atribuir o endereço IP de Olá que está reservado para o cluster de Olá][sap-ha-guide-figure-3013]

  _**Figura 24:** atribuir o endereço IP Olá que está reservado para o cluster de Olá_

6.  Coloque o nome de anfitrião virtual de cluster de Olá online.

  ![Figura 25: O serviço de núcleo de Cluster está operacional e em execução e com Olá corrija o endereço IP][sap-ha-guide-figure-3014]

  _**Figura 25:** serviço de núcleo de Cluster está operacional e em execução e com Olá corrija o endereço IP_

7.  Adicione Olá segundo nó de cluster.

  Agora que o serviço de cluster de núcleos de Olá está a funcionar, pode adicionar o segundo nó de cluster Olá.

  ![Figura 26: Adicionar Olá segundo o nó de cluster][sap-ha-guide-figure-3015]

  _**Figura 26:** adicionar Olá segundo cluster nó_

8.  Introduza um nome de anfitrião do nó de cluster Olá segundo.

  ![Figura 27: Introduza o nome de anfitrião de nó Olá segundo cluster][sap-ha-guide-figure-3016]

  _**Figura 27:** Enter Olá segundo cluster nó nome de anfitrião_

  > [!IMPORTANT]
  > Se possível esse Olá **adicionar todos os clusters de toohello o armazenamento elegível** caixa de verificação está **não** selecionado.  
  >
  >

  ![Figura 28: Não selecione a caixa de verificação Olá][sap-ha-guide-figure-3017]

  _**Figura 28:** fazer **não** Olá, selecione a caixa de verificação_

  Pode ignorar avisos sobre o quórum e de discos. Iremos definir disco de Olá quórum e partilha hello mais tarde, conforme descrito em [instalar SIOS DataKeeper Cluster Edition para partilha de disco em cluster SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Figura 29: Ignorar avisos sobre o quórum de disco Olá][sap-ha-guide-figure-3018]

  _**Figura 29:** ignorar avisos sobre o quórum de disco Olá_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Configurar um testemunho de partilha de ficheiros do cluster

Configurar um testemunho de partilha de ficheiros do cluster envolve estas tarefas:

- Criar uma partilha de ficheiros
- A definição de quórum de testemunho de partilha de ficheiros de Olá no Gestor de clusters de ativação pós-falha

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Criar uma partilha de ficheiros

1.  Selecione um testemunho de partilha de ficheiros em vez de um disco de quórum. SIOS DataKeeper suportar esta opção.

  Nos exemplos de Olá neste artigo, Olá testemunho de partilha de ficheiros está num servidor DNS/do Active Directory de Olá que está em execução no Azure. Olá testemunho de partilha de ficheiro é denominado **domcontr-0**. Porque iria configurou um tooAzure de ligação VPN (através de VPN de Site para Site ou Azure ExpressRoute), o DNS do Active Directory/serviço é no local e não é um ficheiro de toorun adequado testemunho de partilha.

  > [!NOTE]
  > Se o serviço DNS/do Active Directory é executado apenas no local, não configure o testemunho de partilha de ficheiros no sistema de operativo de Active Directory/DNS Windows hello que está a ser executado no local. Latência de rede entre nós de cluster em execução no Azure e o DNS/do Active Directory no local poderá ser demasiado grande e causar problemas de conectividade. Ser se tooconfigure Olá testemunho de partilha ficheiros numa máquina virtual do Azure que está a executar o nó de cluster toohello fechar.  
  >
  >

  unidade de quórum Olá necessita de, pelo menos, 1.024 MB de espaço livre. Recomendamos 2.048 MB de espaço livre de disco de quórum Olá.

2.  Adicione o objeto de nome de cluster Olá.

  ![Figura 30: Atribua permissões de Olá numa partilha de Olá para o objeto de nome de cluster Olá][sap-ha-guide-figure-3019]

  _**Figura 30:** atribuir permissões de Olá numa partilha de Olá para o objeto de nome de cluster Olá_

  Certifique-se de que as permissões de Olá incluem dados de toochange de autoridade de Olá numa partilha de Olá para o objeto de nome de cluster Olá (no nosso exemplo, **pr1-ascs-vir$**).

3.  tooadd Olá cluster nome objeto toohello lista, selecione **adicionar**. Alterar o filtro de Olá toocheck para objetos de computador, no toothose adição mostrado na figura 31.

  ![Figura 31: Alterar computadores de tooinclude Olá tipos de objeto][sap-ha-guide-figure-3020]

  _**Figura 31:** alterar computadores de tooinclude Olá tipos de objeto_

  ![Figura 32: Selecione a caixa de verificação de computadores de Olá][sap-ha-guide-figure-3021]

  _**Figura 32:** Olá selecione **computadores** caixa de verificação_

4.  Introduza o objeto de nome de cluster Olá conforme mostrado na figura 31. Porque o registo de Olá já tiver sido criado, pode alterar as permissões de Olá, conforme mostrado na figura 30.

5.  Selecione Olá **segurança** separador da partilha de Olá e, em seguida, defina mais detalhadas permissões para o objeto de nome de cluster Olá.

  ![Figura 33: Definir atributos de segurança de Olá do objeto de nome de cluster Olá no quórum de partilha de ficheiros de Olá][sap-ha-guide-figure-3022]

  _**Figura 33:** definir atributos de segurança de Olá do objeto de nome de cluster Olá no quórum de partilha de ficheiros de Olá_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Definir quórum de testemunho de partilha de ficheiros de Olá no Gestor de clusters de ativação pós-falha

1.  Abra Olá Assistente de definição de quórum de configurar.

  ![Figura 34: Iniciar Olá Assistente de definição de quórum de Cluster de configurar][sap-ha-guide-figure-3023]

  _**Figura 34:** início Olá configurar Assistente de definição de quórum de Cluster_

2.  No Olá **selecione configuração do quórum** página, selecione **selecionar testemunho de quórum Olá**.

  ![35 figura: Pode escolher entre configurações de quórum][sap-ha-guide-figure-3024]

  _**Figura 35:** configurações de quórum, pode escolher entre_

3.  No Olá **selecionar testemunho de quórum** página, selecione **configurar um testemunho de partilha de ficheiros**.

  ![Figura 36: Testemunho de partilha de ficheiros de Olá selecione][sap-ha-guide-figure-3025]

  _**Figura 36:** selecione Olá testemunho de partilha de ficheiros_

4.  Introduza a partilha de ficheiros de toohello de caminho UNC Olá (no nosso exemplo, \\domcontr 0\FSW). uma lista de alterações de Olá que pode fazer, selecione de toosee **seguinte**.

  ![Figura 37: Definir localização de partilha de ficheiros de Olá para partilha de testemunho Olá][sap-ha-guide-figure-3026]

  _**Figura 37:** Definir localização de partilha de ficheiros de Olá para partilha de testemunho Olá_

5.  Selecione as alterações de Olá que pretende e, em seguida, selecione **seguinte**. Terá de toosuccessfully reconfigurar a configuração de cluster Olá conforme mostrado na figura 38.  

  ![38 figura: Se tiver reconfigurado cluster Olá de confirmação][sap-ha-guide-figure-3027]

  _**Figura 38:** confirmação que tiver reconfigurado cluster Olá_

Depois de instalar com êxito Olá Cluster de ativação pós-falha do Windows, as alterações precisam de toobe efetuada tooconditions de deteção de ativação pós-falha do toosome limiares tooadapt no Azure. Olá toobe parâmetros alterado estão documentados neste blogue: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Partindo do princípio de que as duas VMs que criar Olá configuração de Cluster do Windows para ASCS/SCS na estão Olá mesma sub-rede, hello parâmetros seguintes necessário toobe alterado toothese valores:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Estas definições foram testadas com os clientes e fornecidas toobe um compromisso boa resiliente suficiente no lado Olá. No Olá por outro lado essas definições foram fornecer rápido suficiente ativação pós-falha em condições de erro real em caso de falha SAP, software ou o nó/VM. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar SIOS DataKeeper Cluster Edition para partilha de disco de cluster em SAP ASCS/SCS Olá

Agora tem uma configuração de Clustering de ativação pós-falha do Windows Server no Azure. No entanto, tooinstall uma instância do SAP ASCS/SCS, precisa de um recurso de disco partilhado. Não é possível criar recursos de disco Olá partilhado que terá no Azure. SIOS DataKeeper Cluster Edition é uma solução de terceiros podem utilizar recursos de disco toocreate partilhado.

Instalar SIOS DataKeeper Cluster Edition para Olá SAP ASCS/SCS partilha de disco em cluster envolve estas tarefas:

- Adicionar Olá .NET Framework 3.5
- Instalar SIOS DataKeeper
- Configurar SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Adicionar Olá .NET Framework 3.5
Olá o Microsoft .NET Framework 3.5 automaticamente não está ativado ou não está instalado no Windows Server 2012 R2. Uma vez SIOS DataKeeper requer Olá toobe de .NET Framework em todos os nós que instala DataKeeper no, tem de instalar Olá .NET Framework 3.5 no sistema de operativo convidado Olá de todas as máquinas virtuais no cluster de Olá.

Existem Olá duas formas de tooadd .NET Framework 3.5:

- Utilize o assistente Olá adicionar funções e funcionalidades no Windows conforme mostrado na figura 39.

  ![Figura 39: Instalar Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades][sap-ha-guide-figure-3028]

  _**Figura 39:** Olá de instalação do .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades_

  ![Figura 40: Progresso da instalação de barra quando instala Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades][sap-ha-guide-figure-3029]

  _**Figura 40:** progresso da instalação de barra quando instala Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades_

- Utilize Olá ferramenta da linha de comandos dism.exe. Para este tipo de instalação, terá de diretório de SxS Olá tooaccess no Olá suporte de instalação do Windows. Na linha de comandos elevada, escreva:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a>Instalar SIOS DataKeeper

Instale SIOS DataKeeper Cluster Edition em cada nó no cluster de Olá. toocreate virtual armazenamento partilhado com SIOS DataKeeper, crie um espelho sincronizado e, em seguida, simular o armazenamento partilhado de cluster.

Antes de instalar o software SIOS Olá, criar utilizador de domínio Olá **DataKeeperSvc**.

> [!NOTE]
> Adicionar Olá **DataKeeperSvc** utilizador toohello **Administrador Local** grupo em ambos os nós de cluster.
>
>

tooinstall SIOS DataKeeper:

1.  Instale o software SIOS Olá em ambos os nós de cluster.

  ![Instalador SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Primeira página do Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3031]

  _**Figura 41:** primeira página do Olá SIOS DataKeeper instalação_

2.  Na caixa de diálogo de Olá mostrada na figura 42, selecione **Sim**.

  ![Figura 42: DataKeeper informa-o se um serviço será desativado][sap-ha-guide-figure-3032]

  _**Figura 42:** DataKeeper informa que um serviço vai ser desativado_

3.  Na caixa de diálogo de Olá mostrada na figura 43, recomendamos que selecione **conta de domínio ou servidor**.

  ![Figura 43: Seleção de utilizador para SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Figura 43:** seleção do utilizador para SIOS DataKeeper_

4.  Introduza o nome de utilizador da conta de domínio de Olá e palavras-passe que criou para SIOS DataKeeper.

  ![Figura 44: Introduza o nome de utilizador de domínio Olá e a palavra-passe para Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3034]

  _**Figura 44:** introduza o nome de utilizador de domínio Olá e a palavra-passe para Olá SIOS DataKeeper instalação_

5.  Instale a chave de licença de Olá na sua instância SIOS DataKeeper conforme mostrado na figura 45.

  ![Figura 45: Introduza a chave de licença de SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Figura 45:** introduzir a chave de licença SIOS DataKeeper_

6.  Quando lhe for pedido, reinicie a máquina virtual de Olá.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>Configurar SIOS DataKeeper

Depois de instalar SIOS DataKeeper em ambos os nós, terá de configuração de Olá toostart. objetivo Olá configuração Olá é a replicação de dados síncrona toohave entre discos adicionais Olá ligado tooeach das máquinas de virtuais Olá.

1.  Iniciar Olá DataKeeper gestão e a ferramenta de configuração e, em seguida, selecione **ligar servidor**. (Na figura 46, esta opção está dentro de um círculo vermelho.)

  ![Figura 46: Ferramenta de configuração e SIOS DataKeeper gestão][sap-ha-guide-figure-3036]

  _**Figura 46:** ferramenta SIOS DataKeeper gestão e configuração_

2.  Introduza Olá nome ou endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e, um segundo passo, o segundo nó de Olá.

  ![Figura 47: Nome de Olá de inserção ou o endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e um segundo passo, o segundo nó de Olá][sap-ha-guide-figure-3037]

  _**Figura 47:** nome Olá de inserção ou endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e um segundo passo, o segundo nó de Olá_

3.  Crie tarefa de replicação de Olá entre dois nós de Olá.

  ![Figura 48: Criar uma tarefa de replicação][sap-ha-guide-figure-3038]

  _**Figura 48:** criar uma tarefa de replicação_

  Um assistente orienta-o processo de Olá de criação de uma tarefa de replicação.
4.  Defina nome Olá, o endereço de TCP/IP e o volume do disco do nó de origem Olá.

  ![Figura 49: Definir o nome de Olá da tarefa de replicação de Olá][sap-ha-guide-figure-3039]

  _**Figura 49:** definir o nome de Olá da tarefa de replicação de Olá_

  ![Figura 50: Definir a base de dados de Olá para o nó de Olá, que deve ser o nó de origem atual Olá][sap-ha-guide-figure-3040]

  _**Figura 50:** definir Olá base de dados para o nó de Olá, que deve ser o nó de origem atual Olá_

5.  Defina nome Olá, o endereço de TCP/IP e o volume de disco do nó de destino Olá.

  ![Figura 51: Definir os dados de base de Olá para o nó de Olá, que deve ser o nó de destino atual Olá][sap-ha-guide-figure-3041]

  _**Figura 51:** definir Olá base de dados para o nó de Olá, que deve ser o nó de destino atual Olá_

6.  Defina os algoritmos de compressão Olá. No nosso exemplo, recomendamos que comprimir o fluxo de replicação de Olá. Especialmente em situações de ressincronização, Olá a compressão de fluxo de replicação de Olá reduz significativamente o tempo de ressincronização. Tenha em atenção que a compressão utiliza recursos de CPU e RAM Olá de uma máquina virtual. À medida que aumenta a taxa de compressão Olá, por isso, Olá volume dos recursos de CPU utilizado. Também pode ajustar esta definição mais tarde.

7.  Precisa de outra definição toocheck é se ocorre a replicação de Olá assíncrona ou síncrona. *Quando protege configurações de SAP ASCS/SCS, tem de utilizar replicação síncrona*.  

  ![Figura 52: Definir os detalhes de replicação][sap-ha-guide-figure-3042]

  _**Figura 52:** definir os detalhes de replicação_

8.  Defina se o volume de Olá que é replicado pela tarefa de replicação de Olá deve ser representado tooa configuração de cluster Clustering de ativação pós-falha do Windows Server como um disco partilhado. Para a configuração de SAP ASCS/SCS Olá, selecione **Sim** para que o Windows hello cluster vê Olá volume replicada como um disco partilhado que possa utilizar como um volume de cluster.

  ![Figura 53: Selecione Sim tooset Olá replicado volume como volume de cluster][sap-ha-guide-figure-3043]

  _**Figura 53:** selecione **Sim** tooset Olá replicado volume como um volume de cluster_

  Após a criação do volume de Olá, a ferramenta de configuração e gestão DataKeeper Olá mostra que a tarefa de replicação Olá está ativa.

  ![Figura 54 em que: DataKeeper espelhamento síncrono de Olá SAP ASCS/SCS partilha de disco está ativo][sap-ha-guide-figure-3044]

  _**Figura 54 em que:** DataKeeper espelhamento síncrono para hello SAP ASCS/SCS partilhar disco está ativo_

  Gestor de clusters de ativação pós-falha mostra agora disco Olá como um disco de DataKeeper, conforme mostrado na figura 55.

  ![Figura 55: O Gestor de clusters de ativação pós-falha mostra disco Olá que foram replicada para DataKeeper][sap-ha-guide-figure-3045]

  _**Figura 55:** Gestor de clusters de ativação pós-falha mostra disco Olá esse DataKeeper replicado_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar o sistema de SAP NetWeaver Olá

Iremos não descrevem o programa de configuração do Olá DBMS porque setups variam consoante Olá sistema DBMS que utiliza. No entanto, partimos do princípio que preocupações de elevada disponibilidade com Olá DBMS são tratadas com funcionalidades de Olá fornecedores DBMS diferentes Olá suportem do Azure. Por exemplo, Always On ou espelhamento de base de dados para o SQL Server e Oracle Data Guard para bases de dados Oracle. Cenário de Olá que utilizamos neste artigo, iremos não adicionar mais proteção toohello DBMS.

Não existem não existem considerações especiais quando os diferentes serviços DBMS interagem com este tipo de configuração em cluster do SAP ASCS/SCS no Azure.

> [!NOTE]
> procedimentos de instalação de Olá do SAP NetWeaver ABAP sistemas, sistemas de Java e sistemas ABAP + Java são quase idênticos. diferença mais significativa Olá é que um sistema de SAP ABAP tem uma instância ASCS. Olá sistema SAP Java tem uma instância SCS. Olá sistema SAP ABAP + Java tem uma instância ASCS e Olá de uma instância SCS em execução no mesmo grupo de cluster de ativação pós-falha da Microsoft. Todas as diferenças de instalação para cada pilha de instalação do SAP NetWeaver explicitamente são mencionadas. Pode assumir que são Olá todas as outras partes do mesmo.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Instale o SAP com uma instância ASCS/SCS de elevada disponibilidade

> [!IMPORTANT]
> Certifique-se de não tooplace sua página de ficheiros no DataKeeper espelhada volumes. DataKeeper não suporta volumes espelhados. Pode deixar o ficheiro de paginação na unidade temporária Olá D de uma máquina virtual do Azure, que é Olá predefinido. Se este não estiver lá, mova Olá Windows página ficheiro toodrive d: da sua máquina virtual do Azure.
>
>

Instalação do SAP com uma instância ASCS/SCS de elevada disponibilidade envolve estas tarefas:

- Criar um nome de anfitrião virtual para a instância de SAP ASCS/SCS Olá em cluster
- Instalar Olá SAP primeiro nó de cluster
- Modificar o perfil SAP Olá da instância ASCS/SCS Olá
- Adicionar uma porta de pesquisa
- Ao abrir a porta da sonda Olá Windows firewall

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Criar um nome de anfitrião virtual para a instância de SAP ASCS/SCS Olá em cluster

1.  No Gestor de DNS do Windows hello, crie uma entrada DNS para o nome de anfitrião virtual Olá da instância ASCS/SCS Olá.

  > [!IMPORTANT]
  > Olá endereço IP que atribuir o nome de anfitrião virtual toohello de Olá ASCS/SCS instância tem de ser Olá mesmo como endereço IP Olá que atribuiu tooAzure Balanceador de carga (**<*SID*> - lb - ascs **).  
  >
  >

  Olá, endereço IP do nome de anfitrião de SAP ASCS/SCS virtual Olá (**pr1-ascs-sap**) é Olá mesmo como endereço IP de Olá do Balanceador de carga do Azure (**pr1-lb-ascs**).

  ![Figura 56: Definir a entrada DNS de Olá para o nome virtual do cluster de SAP ASCS/SCS Olá e o endereço de TCP/IP][sap-ha-guide-figure-3046]

  _**Figura 56:** definir Olá entrada DNS para o nome virtual do cluster de SAP ASCS/SCS Olá e o endereço de TCP/IP_

2.  toodefine Olá atribuído toohello anfitrião virtual nome de endereço IP, selecione **Gestor de DNS** > **domínio**.

  ![Figura 57: Novo nome virtual e o endereço de TCP/IP para a configuração de cluster do SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Figura 57:** para configuração de cluster do SAP ASCS/SCS de endereços novo nome virtual e TCP/IP_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar Olá SAP primeiro nó de cluster

1.  Executar Olá primeiro cluster nó opção no nó de cluster A. Por exemplo, num Olá **pr1-ascs-0** anfitrião.
2.  portas de predefinição de Olá tookeep para Olá Azure interno Balanceador de carga, selecione:

  * **Sistema ABAP**: **ASCS** instância número **00**
  * **Sistema de Java**: **SCS** instância número **01**
  * **Sistema ABAP + Java**: **ASCS** instância número **00** e **SCS** instância número **01**

  instância toouse números à 00 para Olá ABAP ASCS instância e 01 para a instância de Java SCS Olá, primeiro tem de toochange Olá do Azure de carga interno balanceador predefinido de balanceamento de carga regras, descritas em [carga do alteração Olá ASCS/SCS predefinido balanceamento de regras de Balanceador de carga interno do Azure Olá][sap-ha-guide-8.9].

Olá seguintes algumas tarefas não são descritas na documentação de instalação de SAP Olá padrão.

> [!NOTE]
> Olá documentação de instalação do SAP descreve como tooinstall Olá primeiro nó de cluster ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar o perfil SAP Olá da instância ASCS/SCS Olá

É necessário tooadd um novo parâmetro de perfil. parâmetro de perfil Olá impede que as ligações entre os processos de trabalho do SAP e o servidor de colocar em fila de Olá fechar quando estão inativos há demasiado tempo. Iremos mencionado no cenário de problema de Olá [adicionar entradas de registo em ambos os nós de cluster de instância de SAP ASCS/SCS Olá][sap-ha-guide-8.11]. Na secção, introduzimos também dois parâmetros de ligação de TCP/IP básicos do alterações toosome. No segundo passo, terá de tooset Olá colocar em fila servidor toosend um `keep_alive` assinalar para que as ligações de Olá não atingiu o limiar de inatividade do Balanceador de carga interno do Azure Olá.

Olá toomodify perfil SAP da instância ASCS/SCS Olá:

1.  Adicione este toohello de parâmetro de perfil perfil de instância do SAP ASCS/SCS:

  ```
  enque/encni/set_so_keepalive = true
  ```
  No nosso exemplo, o caminho de Olá é:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Por exemplo, perfil de instância do SAP SCS toohello e caminho correspondente:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  alterações de Olá tooapply, reiniciar a instância de SAP ASCS /SCS de Olá.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Adicionar uma porta de pesquisa

Utilize o trabalho de configuração ao cluster completo do Olá de toomake do Balanceador de carga interno Olá sonda funcionalidade com o Balanceador de carga do Azure. Balanceador de carga interno do Azure Olá normalmente distribui a carga de trabalho de entrada Olá equitativamente entre participantes máquinas virtuais. No entanto, isto não funcionará em algumas configurações de cluster porque apenas uma instância está ativa. Olá outra instância for passiva e não pode aceitar qualquer carga de trabalho Olá. Uma funcionalidade de pesquisa ajuda-o quando atribui de Balanceador de carga interno do Azure Olá trabalham instância ativa tooan apenas. Com a funcionalidade de pesquisa de Olá, o Balanceador de carga interno Olá pode detetar as instâncias ativas e apenas Olá instância com carga de trabalho Olá de destino, em seguida.

tooadd uma porta de pesquisa:

1.  Verifique Olá atual **ProbePort** definição executando o seguinte comando do PowerShell de Olá. Executá-lo de dentro de uma das máquinas virtuais Olá numa configuração de cluster Olá.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Defina uma porta de pesquisa. número de porta de pesquisa do Olá predefinido é **0**. No nosso exemplo, utilizamos a porta da sonda **62000**.

  ![Figura 58: porta Olá da sonda de configuração de cluster é 0 por predefinição][sap-ha-guide-figure-3048]

  _**Figura 58:** porta de pesquisa de configuração de cluster predefinida Olá é 0_

  número de porta de Olá está definido nos modelos de SAP Azure Resource Manager. Pode atribuir o número de porta de Olá no PowerShell.

  tooset um novo valor ProbePort Olá  **SAP <*SID*> IP * * recurso de cluster, execute o seguinte script do PowerShell de Olá. Atualize as variáveis de PowerShell Olá para o seu ambiente. Após a execução do script Olá, será pedido toorestart Olá SAP grupo tooactivate Olá as alterações de cluster.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Depois de colocar Olá  **SAP <*SID*> * * online a função de cluster, certifique-se de que **ProbePort** está definido toohello novo valor.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Sonda a porta de cluster Olá depois de definir o novo valor de Olá][sap-ha-guide-figure-3049]

  _**Figura 59:** sonda a porta de cluster Olá depois de definir o novo valor de Olá_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra a porta da sonda Olá Windows firewall

É necessário tooopen uma porta de sonda de firewall do Windows em ambos os nós de cluster. Utilize Olá seguinte script tooopen uma porta de sonda de firewall do Windows. Atualize as variáveis de PowerShell Olá para o seu ambiente.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Olá **ProbePort** estiver definido demasiado**62000**. Agora pode aceder à partilha de ficheiros de Olá  **\\\ascsha-clsap\sapmnt** dos outros anfitriões, tais como de **ascsha dbas**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar a instância de base de dados de Olá

base de dados do tooinstall Olá instância, siga o processo de Olá descrito em Olá documentação de instalação do SAP.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar o segundo nó de cluster Olá

tooinstall Olá segundo cluster, siga os passos de Olá no Olá guia de instalação do SAP.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Alterar tipo de início de Olá de instância de serviço do Windows do SAP ERS Olá

Alterar o tipo de início de Olá de Olá serviço Windows do SAP ERS demasiado**automático (início atrasado)** em ambos os nós de cluster.

![Figura 60: Altere o tipo de serviço Olá para Olá SAP ERS instância toodelayed automática][sap-ha-guide-figure-3050]

_**Figura 60:** alterar tipo de serviço Olá Olá SAP ERS instância toodelayed automática_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Olá SAP primário o servidor de aplicações

Instalar instância do servidor de aplicação principal (PAS) Olá <*SID*> - di - 0, na máquina virtual Olá que tiver designado toohost Olá PAS. Não existem nenhumas dependências nas definições específicas do DataKeeper ou do Azure.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Olá SAP adicionais o servidor de aplicações

Instale um servidor SAP aplicação adicionais (AAS) em todas as máquinas de virtuais Olá que lhe tiver designado toohost uma instância de servidor de aplicações SAP. Por exemplo, num <*SID*> - di - 1 demasiado <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Isto conclusão da instalação de Olá de um sistema de SAP NetWeaver de elevada disponibilidade. Em seguida, prossiga com a ativação pós-falha de teste.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testar a ativação pós-falha de instância do SAP ASCS/SCS Olá e replicação SIOS
É fácil tootest e monitorizar uma ativação pós-falha de instância do SAP ASCS/SCS e a replicação de discos SIOS utilizando o Gestor de clusters de ativação pós-falha e a ferramenta de configuração e gestão de DataKeeper SIOS Olá.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>Instância do SAP ASCS/SCS está em execução no nó de cluster A

Olá **SAP PR1** grupo de cluster está em execução no nó de cluster A. Por exemplo, num **pr1-ascs-0**. Atribuir a unidade de disco de Olá partilhado S, que faz parte do Olá **SAP PR1** grupo e utiliza a que instância ASCS/SCS Olá, toocluster recomeço de nó do cluster

![Figura 61: Gestor de clusters de ativação pós-falha: grupo de cluster do SAP < SID > olá está em execução no nó de cluster A][sap-ha-guide-figure-5000]

_**Figura 61:** Gestor de clusters de ativação pós-falha: Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster A_

Olá SIOS DataKeeper gestão e a ferramenta de configuração, pode ver esse disco partilhado de Olá os dados são replicados em sincronia de Olá origem volume unidade S no nó de cluster de uma unidade de volume de destino S de toohello num nó de cluster B. Por exemplo, são replicado desde **pr1-ascs-0 [10.0.0.40]** demasiado**pr1-ascs-1 [10.0.0.41]**.

![Figura 62: No SIOS DataKeeper, replicar volume local Olá do nó de cluster de um nó de toocluster B][sap-ha-guide-figure-5001]

_**Figura 62:** no SIOS DataKeeper, replicar volume local Olá a partir do nó de cluster de um nó de toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>A ativação pós-falha do nó A toonode B

1.  Escolha uma das tooinitiate opções uma ativação pós-falha da Olá SAP <*SID*> grupo de cluster de nó A toocluster do nó do cluster b:
  - Utilize o Gestor de clusters de ativação pós-falha  
  - Utilizar o PowerShell do Cluster de ativação pós-falha

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Reiniciar um nó de cluster no sistema de operativo convidado de Windows hello (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).  
3.  Reinicie o nó de cluster A partir do portal do Azure de Olá (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).  
4.  Reiniciar um nó de cluster utilizando o Azure PowerShell (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).

  Após a ativação pós-falha, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B. Por exemplo, que é executada **pr1-ascs-1**.

  ![Figura 63: No Gestor de clusters de ativação pós-falha, grupo de cluster do SAP < SID > olá está em execução no nó de cluster B][sap-ha-guide-figure-5002]

  _**Figura 63**: na ativação pós-falha Gestor de clusters, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B_

  Olá disco partilhado está agora montado no cluster de nó B. SIOS DataKeeper está a replicar dados do disco de volume de origem S no cluster nó B tootarget volume unidade S no nó de cluster A. Por exemplo, está a replicar de **pr1-ascs-1 [10.0.0.41]** demasiado**pr1-ascs-0 [10.0.0.40]**.

  ![Figura 64: SIOS DataKeeper replica volume local Olá nó B toocluster do nó do cluster A][sap-ha-guide-figure-5003]

  _**Figura 64:** SIOS DataKeeper replica volume local Olá nó B toocluster do nó do cluster A_
