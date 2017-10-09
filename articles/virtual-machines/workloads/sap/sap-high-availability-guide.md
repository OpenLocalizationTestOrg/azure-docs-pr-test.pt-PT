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
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="56953-103">Azure máquinas virtuais elevada disponibilidade para SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="56953-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

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



<span data-ttu-id="56953-109">Máquinas virtuais do Azure é a solução de Olá para organizações que precisam de computação, armazenamento e recursos de rede, na altura mínima e sem ciclos de aprovisionamento demorado.</span><span class="sxs-lookup"><span data-stu-id="56953-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="56953-110">Pode utilizar máquinas virtuais do Azure toodeploy aplicações clássico como baseado em SAP NetWeaver ABAP, Java e uma pilha ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="56953-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="56953-111">Expanda a fiabilidade e disponibilidade sem recursos no local adicionais.</span><span class="sxs-lookup"><span data-stu-id="56953-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="56953-112">Máquinas virtuais do Azure suporta uma conectividade entre instalações, pelo que pode integrar Virtual Machines do Azure domínios no local, nuvens privadas e horizontal do sistema SAP da sua organização.</span><span class="sxs-lookup"><span data-stu-id="56953-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="56953-113">Neste artigo, vamos abordar Olá passos que que pode tomar toodeploy sistemas SAP de elevada disponibilidade no Azure utilizando o modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="56953-114">Vamos guiá-lo estas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="56953-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="56953-115">Localizar Olá direita guias de SAP notas e instalação listados no Olá [recursos] [ sap-ha-guide-2] secção.</span><span class="sxs-lookup"><span data-stu-id="56953-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="56953-116">Este artigo complementa a documentação de instalação do SAP e notas de SAP, que são recursos primário Olá e que podem ajudar a instalar e implementar o software de SAP plataformas específicas.</span><span class="sxs-lookup"><span data-stu-id="56953-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="56953-117">Saiba Olá diferenças e o modelo de implementação clássico do Azure de Olá do modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="56953-118">Saiba mais sobre os modos de quórum de Clustering de ativação pós-falha do Windows Server, pelo que pode selecionar o modelo de Olá que é mais adequado para a sua implementação do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="56953-119">Saiba mais sobre o Windows Server Clustering de ativação pós-falha partilhado armazenamento nos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="56953-120">Saiba como toohelp proteger único ponto de falha componentes, como o Advanced negócio Application Programming (ABAP) SAP Central serviços (ASCS) / SAP Central serviços (SCS) e sistemas de gestão de base de dados (DBMS) e os componentes redundantes como o SAP Servidor de aplicações, no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="56953-121">Siga um exemplo passo a passo de uma instalação e configuração de um sistema SAP de elevada disponibilidade num cluster de Clustering de ativação pós-falha do Windows Server no Azure utilizando o Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="56953-122">Saiba mais sobre toouse necessários passos adicionais Clustering de ativação pós-falha no Windows Server no Azure, mas que não são necessários numa implementação no local.</span><span class="sxs-lookup"><span data-stu-id="56953-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="56953-123">toosimplify implementação e configuração, neste artigo, utilizamos Olá modelos do Resource Manager de elevada disponibilidade de três camadas SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="56953-124">modelos de Olá automatizam a implementação de Olá toda a infraestrutura que necessita para um sistema SAP de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56953-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="56953-125">infraestrutura de Olá também suporta o dimensionamento de SAP aplicação desempenho Standard (SAPS) do seu sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="56953-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56953-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="56953-127">Antes de começar, certifique-se de que cumpre os pré-requisitos de Olá descritas Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="56953-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="56953-128">Além disso, ser toocheck se todos os recursos listados em Olá [recursos] [ sap-ha-guide-2] secção.</span><span class="sxs-lookup"><span data-stu-id="56953-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="56953-129">Neste artigo, utilizamos modelos Azure Resource Manager para [três camadas SAP NetWeaver utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="56953-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="56953-130">Para obter uma descrição úteis de modelos, consulte [modelos SAP Azure Resource Manager](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="56953-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="56953-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Recursos</span><span class="sxs-lookup"><span data-stu-id="56953-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="56953-132">Estes artigos abrangem implementações SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="56953-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="56953-133">[Azure máquinas virtuais de planeamento e implementação de SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="56953-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="56953-134">[Implementação de máquinas virtuais do Azure para SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="56953-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="56953-135">[Implementação de DBMS de máquinas virtuais do Azure para SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="56953-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="56953-136">[Azure máquinas virtuais elevada disponibilidade para SAP NetWeaver (deste guia)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="56953-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="56953-137">Sempre que possível, vamos dar-lhe um toohello de ligação, consultar o guia de instalação do SAP (consulte Olá [guias de instalação do SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="56953-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="56953-138">Pré-requisitos e informações sobre o processo de instalação de Olá, da-lo instalação de SAP NetWeaver uma boa ideia tooread Olá orienta cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="56953-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="56953-139">Este artigo abrange apenas as tarefas específicas para sistemas baseados em SAP NetWeaver que pode utilizar com máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="56953-140">Estas notas de SAP são tópico toohello relacionados do SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="56953-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="56953-141">Número de nota</span><span class="sxs-lookup"><span data-stu-id="56953-141">Note number</span></span> | <span data-ttu-id="56953-142">Título</span><span class="sxs-lookup"><span data-stu-id="56953-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="56953-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="56953-143">[1928533]</span></span> |<span data-ttu-id="56953-144">Aplicações SAP no Azure: os produtos e dimensionamento suportados</span><span class="sxs-lookup"><span data-stu-id="56953-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="56953-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="56953-145">[2015553]</span></span> |<span data-ttu-id="56953-146">SAP no Microsoft Azure: suporta a pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56953-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="56953-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="56953-147">[1999351]</span></span> |<span data-ttu-id="56953-148">Avançada de monitorização do Azure para SAP</span><span class="sxs-lookup"><span data-stu-id="56953-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="56953-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="56953-149">[2178632]</span></span> |<span data-ttu-id="56953-150">Chave de monitorização métricas para SAP no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="56953-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="56953-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="56953-151">[1999351]</span></span> |<span data-ttu-id="56953-152">Virtualização no Windows: avançada de monitorização</span><span class="sxs-lookup"><span data-stu-id="56953-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="56953-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="56953-153">[2243692]</span></span> |<span data-ttu-id="56953-154">Utilização do armazenamento SSD Premium do Azure para a instância do SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="56953-155">Saiba mais sobre Olá [limitações das subscrições Azure][azure-subscription-service-limits-subscription], incluindo as limitações de predefinição geral e limitações máximas.</span><span class="sxs-lookup"><span data-stu-id="56953-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="56953-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de elevada disponibilidade com o Azure Resource Manager vs. o modelo de implementação clássico do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="56953-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="56953-157">Olá, Azure Resource Manager e modelos de implementação clássica do Azure são diferentes nos Olá seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="56953-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="56953-158">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="56953-158">Resource groups</span></span>
- <span data-ttu-id="56953-159">Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="56953-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="56953-160">Suporte para cenários de várias SID SAP</span><span class="sxs-lookup"><span data-stu-id="56953-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="56953-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="56953-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="56953-162">No Gestor de recursos do Azure, pode utilizar toomanage de grupos de recurso todos os recursos da aplicação Olá na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="56953-163">Uma abordagem integrada, num grupo de recursos, todos os recursos ter Olá mesmo ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="56953-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="56953-164">Por exemplo, todos os recursos são criados em Olá mesmo tempo e estas são eliminadas quando a Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="56953-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="56953-165">Saiba mais sobre [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="56953-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="56953-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="56953-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="56953-167">No modelo de implementação clássico do Azure Olá, há uma dependência entre o Balanceador de carga interno do Azure Olá (serviço de Azure Load Balancer) e o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="56953-168">Cada Balanceador de carga interno tem um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="56953-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="56953-169">No Gestor de recursos do Azure, tem de todos os recursos do Azure toobe juntar um grupo de recursos do Azure e isto é válido para o Balanceador de carga do Azure, bem como.</span><span class="sxs-lookup"><span data-stu-id="56953-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="56953-170">No entanto, não há nenhum grupo de recursos do Azure toohave necessidade por Balanceador de carga do Azure, por exemplo, um grupo de recursos do Azure pode conter vários balanceadores de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="56953-171">ambiente de Olá é mais simples e mais flexíveis.</span><span class="sxs-lookup"><span data-stu-id="56953-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="56953-172">Suporte para cenários de várias SID SAP</span><span class="sxs-lookup"><span data-stu-id="56953-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="56953-173">No Gestor de recursos do Azure, pode instalar várias SAP sistema identificador (SID) ASCS/SCS instâncias de um cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="56953-174">Instâncias de várias SID são possíveis devido ao suporte para vários endereços IP para cada Balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="56953-175">toouse Olá modelo de implementação clássica do Azure, siga os procedimentos de Olá descritos [SAP NetWeaver no Azure: instâncias de Clustering SAP ASCS/SCS através da utilização de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="56953-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56953-176">Recomendamos vivamente que utilize o modelo de implementação Azure Resource Manager Olá para as instalações de SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="56953-177">Oferece várias vantagens que não estão disponíveis no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="56953-178">Saiba mais sobre o Azure [modelos de implementação][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="56953-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="56953-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Windows Server Clustering de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="56953-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="56953-180">Clustering de ativação pós-falha do Windows Server é foundation Olá de uma instalação de SAP ASCS/SCS de elevada disponibilidade e o DBMS no Windows.</span><span class="sxs-lookup"><span data-stu-id="56953-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="56953-181">Um cluster de ativação pós-falha é um grupo de 1 + n servidores independentes (nós) que trabalham em conjunto de disponibilidade de Olá tooincrease das aplicações e serviços.</span><span class="sxs-lookup"><span data-stu-id="56953-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="56953-182">Se ocorrer uma falha de nó, Clustering de ativação pós-falha do Windows Server calcula o número de Olá de falhas que podem ocorrer, mantendo em simultâneo um bom estado de funcionamento tooprovide aplicações e serviços em cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="56953-183">Pode escolher entre diferentes quórum modos tooachieve clustering de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="56953-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="56953-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Modos de quórum</span><span class="sxs-lookup"><span data-stu-id="56953-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="56953-185">Pode escolher entre quatro modos de quórum ao utilizar o Clustering de ativação pós-falha do Windows Server:</span><span class="sxs-lookup"><span data-stu-id="56953-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="56953-186">**Maioria de nós**.</span><span class="sxs-lookup"><span data-stu-id="56953-186">**Node Majority**.</span></span> <span data-ttu-id="56953-187">Cada nó do cluster de Olá pode votar.</span><span class="sxs-lookup"><span data-stu-id="56953-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="56953-188">as funções de cluster de Olá apenas com a maioria dos votos, ou seja, com mais de metade Olá votos.</span><span class="sxs-lookup"><span data-stu-id="56953-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="56953-189">Recomendamos esta opção para os clusters que tem um número de nós desigual.</span><span class="sxs-lookup"><span data-stu-id="56953-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="56953-190">Por exemplo, três nós num cluster de sete nós podem falhar e Olá cluster stills distribui uma maioria e continua toorun.</span><span class="sxs-lookup"><span data-stu-id="56953-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="56953-191">**Disco maioria de nós e**.</span><span class="sxs-lookup"><span data-stu-id="56953-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="56953-192">Cada nó e um disco designado (um testemunho de disco) no armazenamento de cluster Olá podem votar quando estão disponíveis e na comunicação.</span><span class="sxs-lookup"><span data-stu-id="56953-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="56953-193">as funções de cluster de Olá apenas com a maioria das Olá os votos, ou seja, com mais de metade Olá votos.</span><span class="sxs-lookup"><span data-stu-id="56953-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="56953-194">Este modo faz sentido num ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="56953-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="56953-195">Se nós de meio Olá e disco Olá estão online, cluster Olá permanece em bom estado.</span><span class="sxs-lookup"><span data-stu-id="56953-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="56953-196">**Nó e o ficheiro partilham maioria**.</span><span class="sxs-lookup"><span data-stu-id="56953-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="56953-197">Cada nó de adição cria uma partilha de ficheiros designado (um testemunho de partilha de ficheiros) Olá administrador pode votar, independentemente se encontram disponíveis nós Olá e partilha de ficheiros e na comunicação.</span><span class="sxs-lookup"><span data-stu-id="56953-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="56953-198">as funções de cluster de Olá apenas com a maioria das Olá os votos, ou seja, com mais de metade Olá votos.</span><span class="sxs-lookup"><span data-stu-id="56953-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="56953-199">Este modo faz sentido num ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="56953-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="56953-200">É semelhante toohello nós e o modo de maioria de disco, mas utiliza uma partilha de ficheiros testemunha em vez de um disco testemunha.</span><span class="sxs-lookup"><span data-stu-id="56953-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="56953-201">Este modo é fácil tooimplement, mas se a partilha de ficheiros de Olá propriamente dito não está altamente disponível, este poderá tornar-se um ponto único de falha.</span><span class="sxs-lookup"><span data-stu-id="56953-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="56953-202">**Sem maioria: Disco apenas**.</span><span class="sxs-lookup"><span data-stu-id="56953-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="56953-203">cluster de Olá tem um quórum se um nó estiver disponível e na comunicação com um disco específico no armazenamento de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="56953-204">Apenas Olá nós também em comunicação com esse disco podem associar cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="56953-205">Recomendamos que utilize este modo.</span><span class="sxs-lookup"><span data-stu-id="56953-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="56953-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Server Clustering de ativação pós-falha no local</span><span class="sxs-lookup"><span data-stu-id="56953-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="56953-207">Figura 1 mostra um cluster de dois nós.</span><span class="sxs-lookup"><span data-stu-id="56953-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="56953-208">Se hello falha da ligação de rede entre os nós de Olá e ambos os nós permanecem cópias de segurança e em execução, uma partilha de ficheiro ou de disco de quórum determina nó que vai continuar do cluster de Olá tooprovide aplicações e serviços.</span><span class="sxs-lookup"><span data-stu-id="56953-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="56953-209">nó de Olá que tem o disco de quórum do acesso toohello ou partilha de ficheiros é nó de Olá que garante que os serviços de continuam.</span><span class="sxs-lookup"><span data-stu-id="56953-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="56953-210">Uma vez que este exemplo utiliza um cluster de dois nós, utilizamos Olá nó e o modo de quórum maioria de partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="56953-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="56953-211">Maioria de disco e Olá nó também é uma opção válida.</span><span class="sxs-lookup"><span data-stu-id="56953-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="56953-212">Num ambiente de produção, recomendamos que utilize um disco de quórum.</span><span class="sxs-lookup"><span data-stu-id="56953-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="56953-213">Pode utilizar o armazenamento e de rede toomake de tecnologia de sistema-altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="56953-213">You can use network and storage system technology toomake it highly available.</span></span>

![Figura 1: Exemplo de uma configuração de Clustering de ativação pós-falha do Windows Server para SAP ASCS/SCS no Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="56953-215">_**Figura 1:** exemplo de uma configuração de Clustering de ativação pós-falha do Windows Server para SAP ASCS/SCS no Azure_</span><span class="sxs-lookup"><span data-stu-id="56953-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="56953-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Armazenamento partilhado</span><span class="sxs-lookup"><span data-stu-id="56953-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="56953-217">Figura 1 mostra também um cluster de dois nós de armazenamento partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="56953-218">Um cluster de armazenamento partilhado no local, todos os nós do cluster de Olá detetam armazenamento partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="56953-219">Um mecanismo de bloqueio protege os dados de Olá contra danos.</span><span class="sxs-lookup"><span data-stu-id="56953-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="56953-220">Todos os nós podem detetar se o outro nó falha.</span><span class="sxs-lookup"><span data-stu-id="56953-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="56953-221">Se falhar um nó, o nó restante Olá é proprietários Olá recursos de armazenamento e garante a disponibilidade de Olá dos serviços.</span><span class="sxs-lookup"><span data-stu-id="56953-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-222">Não precisa de discos partilhados para elevada disponibilidade com algumas aplicações DBMS, tal como com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="56953-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="56953-223">SQL Server Always On replica os ficheiros de registo e dados DBMS do disco local do Olá do disco local do toohello de nó de um cluster de outro nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="56953-224">Nesse caso, configuração de cluster do Windows hello não necessita de um disco partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="56953-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Funcionamento em rede e resolução de nomes</span><span class="sxs-lookup"><span data-stu-id="56953-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="56953-226">Computadores cliente alcancem cluster Olá através de um endereço IP virtual e um nome de anfitrião virtual que Olá fornece de servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="56953-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="56953-227">Olá no local nós e servidor DNS de Olá pode processar vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="56953-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="56953-228">Uma configuração típica, utiliza dois ou mais ligações de rede:</span><span class="sxs-lookup"><span data-stu-id="56953-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="56953-229">Armazenamento de toohello uma ligação dedicada</span><span class="sxs-lookup"><span data-stu-id="56953-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="56953-230">Uma ligação de rede interna para o cluster para o heartbeat Olá</span><span class="sxs-lookup"><span data-stu-id="56953-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="56953-231">Uma rede pública que os clientes utilizam tooconnect toohello cluster</span><span class="sxs-lookup"><span data-stu-id="56953-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="56953-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Server Clustering de ativação pós-falha no Azure</span><span class="sxs-lookup"><span data-stu-id="56953-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="56953-233">Em comparação com as implementações de nuvem privada ou metal toobare, Virtual Machines do Azure requer tooconfigure passos adicionais Clustering de ativação pós-falha do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="56953-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="56953-234">Quando criar um disco partilhado de cluster, terá de tooset vários endereços IP e o anfitrião virtual nomes para a instância de SAP ASCS/SCS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="56953-235">Neste artigo, vamos discutir conceitos chave e Olá passos adicionais necessários toobuild um cluster de elevada disponibilidade de serviços central SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="56953-236">Vamos mostrar-lhe como tooset segurança ferramenta de terceiros Olá SIOS DataKeeper e como tooconfigure Olá Azure interno Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56953-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="56953-237">Pode utilizar estas ferramentas toocreate num cluster de ativação pós-falha do Windows com um testemunho de partilha de ficheiros no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: Clustering de ativação pós-falha do Windows Server configuração no Azure sem um disco partilhado][sap-ha-guide-figure-1001]

<span data-ttu-id="56953-239">_**Figura 2:** configuração Clustering de ativação pós-falha do Windows Server no Azure sem um disco partilhado_</span><span class="sxs-lookup"><span data-stu-id="56953-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="56953-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Partilhar o disco no Azure com SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="56953-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="56953-241">Precisa de cluster armazenamento partilhado para uma instância do SAP ASCS/SCS de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56953-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="56953-242">Como os de Setembro de 2016, não oferta Azure armazenamento partilhado que pode utilizar toocreate um cluster de armazenamento partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="56953-243">Pode utilizar o software de terceiros SIOS DataKeeper Cluster Edition toocreate um armazenamento espelhado que simula o armazenamento partilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="56953-244">Olá solução SIOS fornece replicação síncrona de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="56953-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="56953-245">Esta é a forma como pode criar um recurso de disco partilhado para um cluster:</span><span class="sxs-lookup"><span data-stu-id="56953-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="56953-246">Anexe um tooeach de disco adicional de Olá máquinas de virtuais (VMs) numa configuração de cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="56953-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="56953-247">Execute SIOS DataKeeper Cluster Edition em ambos os nós de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56953-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="56953-248">Configure SIOS DataKeeper Cluster Edition para que este reflete o conteúdo de Olá do volume de disco adicionais ligado Olá do volume adicionais disco ligado toohello de máquina virtual de origem de Olá Olá virtual da máquina de destino.</span><span class="sxs-lookup"><span data-stu-id="56953-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="56953-249">SIOS DataKeeper deduz volumes locais Olá origem e de destino e, em seguida, apresenta-los tooWindows do Clustering de ativação pós-falha como um disco partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="56953-250">Obter mais informações [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="56953-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: Configuração de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="56953-252">_**Figura 3:** configuração de Clustering de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="56953-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="56953-253">Não precisa de discos partilhados para elevada disponibilidade com alguns produtos DBMS, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="56953-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="56953-254">SQL Server Always On replica os ficheiros de registo e dados DBMS do disco local do Olá do disco local do toohello de nó de um cluster de outro nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="56953-255">Neste caso, configuração de cluster do Windows hello não necessita de um disco partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="56953-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Resolução de nomes no Azure</span><span class="sxs-lookup"><span data-stu-id="56953-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="56953-257">plataforma de nuvem do Azure Olá não oferece Olá opção tooconfigure endereços IP virtuais, tais como endereços IP flutuante.</span><span class="sxs-lookup"><span data-stu-id="56953-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="56953-258">É necessário um tooset solução alternativa, se um virtual IP endereço tooreach Olá recurso de cluster na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="56953-259">O Azure tem um balanceador de carga interno no Olá serviço de Balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="56953-260">Com o Balanceador de carga interno Olá, os clientes conseguirem contactar o cluster de Olá através de Olá cluster um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="56953-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="56953-261">Terá de Balanceador de carga interno Olá toodeploy no grupo de recursos de Olá que contém nós de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="56953-262">Em seguida, configure todas as portas necessárias reencaminhamento regras com sonda Olá portas Olá interno de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56953-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="56953-263">os clientes de Olá podem ligar através do nome de anfitrião virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="56953-264">servidor DNS Olá resolve o endereço IP de cluster Olá, porta e o Olá carga interno balanceador identificadores toohello o nó ativo do cluster de Olá de reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="56953-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="56953-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver elevada disponibilidade no Azure infraestrutura-como-um-serviço (IaaS)</span><span class="sxs-lookup"><span data-stu-id="56953-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="56953-266">tooachieve SAP elevada de disponibilidade de aplicações, tais como para componentes de software do SAP, terá de Olá tooprotect os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="56953-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="56953-267">Instância de servidor de aplicações SAP</span><span class="sxs-lookup"><span data-stu-id="56953-267">SAP Application Server instance</span></span>
* <span data-ttu-id="56953-268">Instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="56953-269">Servidor DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-269">DBMS server</span></span>

<span data-ttu-id="56953-270">Para obter mais informações sobre como proteger os componentes SAP em cenários de elevada disponibilidade, consulte [Virtual Machines do Azure de planeamento e implementação de SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="56953-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="56953-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Servidor de aplicações SAP de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="56953-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="56953-272">Normalmente, não precisa de uma solução de elevada disponibilidade específica para instâncias de servidor de aplicações SAP e a caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="56953-273">Alcançar a elevada disponibilidade através da redundância e irá configurar várias instâncias de caixa de diálogo em instâncias diferentes Virtual Machines do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="56953-274">Deve ter, pelo menos, duas instâncias de aplicações SAP instaladas em duas instâncias de Virtual Machines do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Servidor de aplicações de elevada disponibilidade SAP][sap-ha-guide-figure-2000]

<span data-ttu-id="56953-276">_**Figura 4:** servidor de aplicações SAP de elevada disponibilidade_</span><span class="sxs-lookup"><span data-stu-id="56953-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="56953-277">Tem de colocar todas as máquinas virtuais que instâncias de servidor de aplicações SAP de anfitrião no Olá mesmo conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="56953-278">Um conjunto de disponibilidade do Azure garante que:</span><span class="sxs-lookup"><span data-stu-id="56953-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="56953-279">Todas as máquinas virtuais fazem parte do Olá mesmo domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="56953-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="56953-280">Por exemplo, um domínio de atualização, certifica-se de que Olá máquinas de virtuais não são atualizadas em Olá simultâneo durante o período de indisponibilidade de manutenção planeada.</span><span class="sxs-lookup"><span data-stu-id="56953-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="56953-281">Todas as máquinas virtuais fazem parte do Olá mesmo domínio de falhas.</span><span class="sxs-lookup"><span data-stu-id="56953-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="56953-282">Por exemplo, um domínio de falhas certifica-se de que as máquinas virtuais são implementadas para que não existe nenhum ponto único de falha afeta a disponibilidade de Olá de todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="56953-283">Saiba mais sobre como demasiado[gerir a disponibilidade de Olá das máquinas virtuais][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="56953-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="56953-284">Apenas para disco não gerido: uma vez que Olá conta do storage do Azure é um potencial ponto único de falha, é importante toohave pelo menos duas contas de armazenamento do Azure, em que são distribuídas, pelo menos, duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="56953-285">Uma configuração ideal, discos Olá de cada máquina virtual que está a executar uma instância de caixa de diálogo SAP seriam implementados numa conta de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="56953-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="56953-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Instância do SAP ASCS/SCS de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="56953-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="56953-287">Figura 5 é um exemplo de uma instância do SAP ASCS/SCS de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56953-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: Instância de elevada disponibilidade SAP ASCS/SCS][sap-ha-guide-figure-2001]

<span data-ttu-id="56953-289">_**Figura 5:** instância de elevada disponibilidade SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="56953-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="56953-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASCS/SCS instância elevada disponibilidade com Clustering de ativação pós-falha no Windows Server no Azure</span><span class="sxs-lookup"><span data-stu-id="56953-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="56953-291">Em comparação com as implementações de nuvem privada ou metal toobare, Virtual Machines do Azure requer tooconfigure passos adicionais Clustering de ativação pós-falha do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="56953-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="56953-292">toobuild num cluster de ativação pós-falha do Windows, terá de um disco de cluster partilhado, vários endereços IP, vários nomes de anfitrião virtual e um balanceador de carga interno do Azure para uma instância do SAP ASCS/SCS de clustering.</span><span class="sxs-lookup"><span data-stu-id="56953-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="56953-293">Vamos discutir em mais detalhe posteriormente no artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-293">We discuss this in more detail later in hello article.</span></span>

![Figura 6: Windows Server Clustering de ativação pós-falha para uma configuração de SAP ASCS/SCS no Azure utilizando SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="56953-295">_**Figura 6:** Clustering de ativação pós-falha no Windows Server para uma configuração de SAP ASCS/SCS no Azure com SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="56953-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="56953-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Instância DBMS de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="56953-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="56953-297">Olá DBMS também é um único ponto de contacto num sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="56953-298">Terá de tooprotect-la utilizando uma solução de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56953-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="56953-299">A figura 7 mostra uma solução de elevada disponibilidade SQL Server Always On no Azure, com Clustering de ativação pós-falha do Windows Server e Olá Azure interno Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="56953-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="56953-300">SQL Server Always On replica os ficheiros de registo e dados DBMS utilizando a sua própria replicação DBMS.</span><span class="sxs-lookup"><span data-stu-id="56953-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="56953-301">Neste caso, a não precisa de discos de cluster partilhados, que simplifica a configuração completa Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![A figura 7: Exemplo de um DBMS de SAP de elevada disponibilidade, com o SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="56953-303">_**A figura 7:** exemplo de um DBMS de SAP de elevada disponibilidade, com o SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="56953-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="56953-304">Para obter mais informações sobre o clustering do SQL Server no Azure utilizando o modelo de implementação Azure Resource Manager Olá, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="56953-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="56953-305">[Configurar o grupo de disponibilidade Always On em Azure Virtual Machines manualmente utilizando o Gestor de recursos] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="56953-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="56953-306">[Configurar um balanceador de carga interno do Azure para um grupo de disponibilidade Always On no Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="56953-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="56953-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Cenários de implementação de elevada disponibilidade de ponto a ponto</span><span class="sxs-lookup"><span data-stu-id="56953-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="56953-308">Cenário de implementação através da arquitetura de modelo de 1</span><span class="sxs-lookup"><span data-stu-id="56953-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="56953-309">Figura 8 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="56953-310">Este cenário é configure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="56953-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="56953-311">Um cluster dedicado é utilizado para a instância de SAP ASCS/SCS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="56953-312">Um cluster dedicado é utilizado para a instância DBMS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="56953-313">Instâncias de servidor de aplicações SAP são implementadas na suas própria VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="56953-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: SAP elevada disponibilidade da arquitetura modelo 1, com o cluster dedicado para ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="56953-315">_**Figura 8:** SAP 1 modelo da arquitetura do elevada disponibilidade, clusters dedicados para ASCS/SCS e DBMS_</span><span class="sxs-lookup"><span data-stu-id="56953-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="56953-316">Cenário de implementação através da arquitetura de modelo de 2</span><span class="sxs-lookup"><span data-stu-id="56953-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="56953-317">A figura 9 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="56953-318">Este cenário é configure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="56953-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="56953-319">Um cluster dedicado é utilizado para **ambos** Olá SAP ASCS/SCS instância e Olá DBMS.</span><span class="sxs-lookup"><span data-stu-id="56953-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="56953-320">Instâncias de servidor de aplicações SAP são implementadas na próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="56953-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: SAP elevada disponibilidade da arquitetura modelo 2, com um cluster dedicado para ASCS/SCS e um cluster dedicado para DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="56953-322">_**Figura 9:** SAP elevada disponibilidade da arquitetura modelo 2, com um cluster dedicado para ASCS/SCS e um cluster dedicado para DBMS_</span><span class="sxs-lookup"><span data-stu-id="56953-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="56953-323">Cenário de implementação através da arquitetura de modelo de 3</span><span class="sxs-lookup"><span data-stu-id="56953-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="56953-324">A figura 10 mostra um exemplo de uma arquitetura de elevada disponibilidade do SAP NetWeaver no Azure para **dois** SAP sistemas, com &lt;SID1&gt; e &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="56953-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="56953-325">Este cenário é configure da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="56953-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="56953-326">Um cluster dedicado é utilizado para **ambos** instância Olá SAP ASCS/SCS SID1 *e* instância Olá SAP ASCS/SCS SID2 (um cluster).</span><span class="sxs-lookup"><span data-stu-id="56953-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="56953-327">Um cluster dedicado é utilizado para DBMS SID1 e outro cluster dedicado é utilizado para DBMS SID2 (dois clusters).</span><span class="sxs-lookup"><span data-stu-id="56953-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="56953-328">As instâncias de servidor de aplicações do SAP para Olá sistema SAP SID1 ter os seus próprios VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="56953-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="56953-329">As instâncias de servidor de aplicações do SAP para Olá sistema SAP SID2 ter os seus próprios VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="56953-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: SAP elevada disponibilidade da arquitetura modelo 3, com um cluster dedicado para instâncias ASCS/SCS diferentes][sap-ha-guide-figure-6003]

<span data-ttu-id="56953-331">_**Figura 10:** SAP elevada disponibilidade da arquitetura modelo 3, com um cluster dedicado para instâncias ASCS/SCS diferentes_</span><span class="sxs-lookup"><span data-stu-id="56953-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="56953-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar a infraestrutura de Olá</span><span class="sxs-lookup"><span data-stu-id="56953-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="56953-333">Preparar a infraestrutura de Olá da arquitetura de modelo de 1</span><span class="sxs-lookup"><span data-stu-id="56953-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="56953-334">Modelos Azure Resource Manager para SAP ajudam a simplificar a implementação dos recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="56953-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="56953-335">modelos de três camadas Olá no Gestor de recursos do Azure também suportam cenários de elevada disponibilidade, tal como 1 da arquitetura do modelo, que tem dois clusters.</span><span class="sxs-lookup"><span data-stu-id="56953-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="56953-336">Cada cluster é um ponto de falha para SAP ASCS/SCS e DBMS SAP único.</span><span class="sxs-lookup"><span data-stu-id="56953-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="56953-337">Aqui é onde pode obter os modelos Azure Resource Manager para o cenário de exemplo de Olá que dita neste artigo:</span><span class="sxs-lookup"><span data-stu-id="56953-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="56953-338">Imagem do Marketplace do Azure</span><span class="sxs-lookup"><span data-stu-id="56953-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="56953-339">Imagem do Marketplace do Azure utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="56953-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="56953-340">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="56953-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="56953-341">Imagem personalizada utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="56953-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="56953-342">infraestrutura de Olá tooprepare para 1 da arquitetura do modelo:</span><span class="sxs-lookup"><span data-stu-id="56953-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="56953-343">No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **SYSTEMAVAILABILITY** caixa, selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="56953-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: Definir os parâmetros do SAP elevada disponibilidade do Azure Resource Manager][sap-ha-guide-figure-3000]

<span data-ttu-id="56953-345">_**Figura 11:** definir os parâmetros do SAP elevada disponibilidade do Azure Resource Manager_</span><span class="sxs-lookup"><span data-stu-id="56953-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="56953-346">criam modelos de Olá:</span><span class="sxs-lookup"><span data-stu-id="56953-346">hello templates create:</span></span>

  * <span data-ttu-id="56953-347">**Máquinas virtuais**:</span><span class="sxs-lookup"><span data-stu-id="56953-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="56953-348">Máquinas de virtuais do servidor de aplicações SAP: <*SAPSystemSID*> - di - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="56953-349">Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*> - ascs - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="56953-350">DBMS cluster: <*SAPSystemSID*> - db - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="56953-351">**Rede de cartões de todas as máquinas virtuais, com os endereços IP associados**:</span><span class="sxs-lookup"><span data-stu-id="56953-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="56953-352"><*SAPSystemSID*> - nic - di - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="56953-353"><*SAPSystemSID*> - nic - ascs - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="56953-354"><*SAPSystemSID*> - nic - db - <*número*></span><span class="sxs-lookup"><span data-stu-id="56953-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="56953-355">**Contas de armazenamento do Azure (apenas discos não geridos)**</span><span class="sxs-lookup"><span data-stu-id="56953-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="56953-356">**Grupos de disponibilidade** para:</span><span class="sxs-lookup"><span data-stu-id="56953-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="56953-357">Máquinas de virtuais do servidor de aplicações SAP: <*SAPSystemSID*> - avset - di</span><span class="sxs-lookup"><span data-stu-id="56953-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="56953-358">Máquinas virtuais de cluster do SAP ASCS/SCS: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="56953-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="56953-359">Máquinas virtuais de cluster DBMS: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="56953-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="56953-360">**Balanceador de carga interno do Azure**:</span><span class="sxs-lookup"><span data-stu-id="56953-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="56953-361">Com todas as portas para a instância ASCS/SCS Olá e endereço IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="56953-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="56953-362">Com todas as portas para o endereço IP e o SQL Server DBMS Olá <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="56953-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="56953-363">**Grupo de segurança de rede**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="56953-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="56953-364">Com um abra toohello de porta de protocolo RDP (Remote Desktop Protocol) externo <*SAPSystemSID*> - ascs - 0 máquina</span><span class="sxs-lookup"><span data-stu-id="56953-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="56953-365">Todos os endereços IP de placas de rede Olá e Balanceadores de carga internos do Azure são **dinâmica** por predefinição.</span><span class="sxs-lookup"><span data-stu-id="56953-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="56953-366">Alterá-los demasiado**estático** endereços IP.</span><span class="sxs-lookup"><span data-stu-id="56953-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="56953-367">Vamos descrever como toodo este artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="56953-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implementar máquinas virtuais com toouse de conectividade (em vários locais) da rede empresarial na produção</span><span class="sxs-lookup"><span data-stu-id="56953-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="56953-369">Para sistemas de produção SAP, implementar máquinas virtuais do Azure com [conectividade de rede empresarial (em vários locais)] [ planning-guide-2.2] através da utilização do Azure Site a Site VPN ou Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="56953-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-370">Pode utilizar a instância de rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="56953-371">rede virtual Olá e sub-rede já tiverem sido criados e preparados.</span><span class="sxs-lookup"><span data-stu-id="56953-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="56953-372">No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **NEWOREXISTINGSUBNET** caixa, selecione **existente**.</span><span class="sxs-lookup"><span data-stu-id="56953-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="56953-373">No Olá **SUBNETID** caixa, adicione a cadeia completa de Olá da sua rede de Azure preparado SubnetID onde planeia toodeploy as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="56953-374">tooget uma lista de todas as sub-redes de rede do Azure, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="56953-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="56953-375">Olá **ID** campo mostra Olá **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="56953-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="56953-376">tooget uma lista de todos os **SUBNETID** valores, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="56953-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="56953-377">Olá **SUBNETID** se parece com isto:</span><span class="sxs-lookup"><span data-stu-id="56953-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="56953-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Implementar instâncias SAP apenas na nuvem para teste e demonstração</span><span class="sxs-lookup"><span data-stu-id="56953-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="56953-379">Pode implementar o sistema SAP de elevada disponibilidade de um modelo de implementação apenas de nuvem.</span><span class="sxs-lookup"><span data-stu-id="56953-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="56953-380">Este tipo de implementação é principalmente útil para casos de utilização de demonstração e teste.</span><span class="sxs-lookup"><span data-stu-id="56953-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="56953-381">Não é adequada para os casos de utilização de produção.</span><span class="sxs-lookup"><span data-stu-id="56953-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="56953-382">No Olá portal do Azure, no Olá **parâmetros** painel, no Olá **NEWOREXISTINGSUBNET** caixa, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="56953-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="56953-383">Deixe Olá **SUBNETID** campo vazio.</span><span class="sxs-lookup"><span data-stu-id="56953-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="56953-384">Olá SAP do Azure Resource Manager modelo cria automaticamente Olá rede virtual do Azure e a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="56953-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-385">Também precisa de toodeploy pelo menos um dedicado a máquina virtual para o Active Directory e DNS no Olá a mesma instância de rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="56953-386">modelo de Olá não crie estas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="56953-387">Preparar a infraestrutura de Olá da arquitetura de modelo de 2</span><span class="sxs-lookup"><span data-stu-id="56953-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="56953-388">Pode utilizar este modelo Azure Resource Manager para SAP toohelp simplificar a implementação de recursos de infraestrutura necessária para SAP da arquitetura modelo 2.</span><span class="sxs-lookup"><span data-stu-id="56953-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="56953-389">Aqui é onde pode obter os modelos Azure Resource Manager para este cenário de implementação:</span><span class="sxs-lookup"><span data-stu-id="56953-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="56953-390">Imagem do Marketplace do Azure</span><span class="sxs-lookup"><span data-stu-id="56953-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="56953-391">Imagem do Marketplace do Azure utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="56953-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="56953-392">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="56953-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="56953-393">Imagem personalizada utilizando discos geridos</span><span class="sxs-lookup"><span data-stu-id="56953-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="56953-394">Preparar a infraestrutura de Olá da arquitetura de modelo de 3</span><span class="sxs-lookup"><span data-stu-id="56953-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="56953-395">Pode preparar infraestrutura Olá e configurar o SAP para **várias SID**.</span><span class="sxs-lookup"><span data-stu-id="56953-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="56953-396">Por exemplo, pode adicionar uma instância adicional do SAP ASCS/SCS para um *existente* configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="56953-397">Para obter mais informações, consulte [configurar uma instância adicional do SAP ASCS/SCS para um toocreate de configuração de cluster existentes uma configuração de várias SID SAP no Gestor de recursos do Azure][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="56953-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="56953-398">Se quiser toocreate um novo cluster de múltiplos SID, pode utilizar Olá várias-SID [modelos de início rápido no GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="56953-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="56953-399">um novo cluster de múltiplos SID toocreate, terá de Olá toodeploy seguintes três modelos:</span><span class="sxs-lookup"><span data-stu-id="56953-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="56953-400">Modelo ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="56953-401">Modelo de base de dados</span><span class="sxs-lookup"><span data-stu-id="56953-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="56953-402">Modelo de servidores de aplicações</span><span class="sxs-lookup"><span data-stu-id="56953-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="56953-403">Olá secções seguintes tem mais detalhes sobre os modelos de Olá e parâmetros de Olá terá tooprovide nos modelos de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="56953-404"><a name="ASCS-SCS-template"></a>Modelo ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="56953-405">modelo ASCS/SCS Olá implementa duas máquinas virtuais que pode utilizar toocreate um cluster de ativação pós-falha do Windows Server que aloja várias instâncias ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="56953-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="56953-406">tooset segurança modelo Olá ASCS/SCS várias-SID, Olá [modelo de várias SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] ou [modelo de várias SID ASCS/SCS utilizando discos geridos] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="56953-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="56953-407">**Prefixo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="56953-407">**Resource Prefix**.</span></span>  <span data-ttu-id="56953-408">Defina o prefixo de recurso Olá, o que é utilizado tooprefix todos os recursos que são criados durante a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="56953-409">Porque os recursos de Olá não pertencer um sistema SAP tooonly, prefixo Olá do recurso de Olá não é Olá SID de um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="56953-410">prefixo de Olá tem de estar entre **três e seis carateres**.</span><span class="sxs-lookup"><span data-stu-id="56953-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="56953-411">**Tipo de pilha**.</span><span class="sxs-lookup"><span data-stu-id="56953-411">**Stack Type**.</span></span> <span data-ttu-id="56953-412">Selecione o tipo de pilha de Olá de Olá sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="56953-413">Dependendo do tipo de pilha Olá, o Balanceador de carga do Azure tem um (ABAP ou apenas Java) ou dois (ABAP + Java) endereços IP privados por sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="56953-414">**Tipo de SO**.</span><span class="sxs-lookup"><span data-stu-id="56953-414">**OS Type**.</span></span> <span data-ttu-id="56953-415">Selecione o sistema de operativo Olá das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="56953-416">**Contagem de sistema do SAP**.</span><span class="sxs-lookup"><span data-stu-id="56953-416">**SAP System Count**.</span></span> <span data-ttu-id="56953-417">Selecione o número de Olá dos sistemas SAP pretende tooinstall neste cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="56953-418">**Disponibilidade do sistema**.</span><span class="sxs-lookup"><span data-stu-id="56953-418">**System Availability**.</span></span> <span data-ttu-id="56953-419">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="56953-419">Select **HA**.</span></span>
  -  <span data-ttu-id="56953-420">**Nome de utilizador de administrador e a palavra-passe de administrador**.</span><span class="sxs-lookup"><span data-stu-id="56953-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="56953-421">Crie um novo utilizador que pode ser utilizado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="56953-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="56953-422">**Novo ou existente sub-rede**.</span><span class="sxs-lookup"><span data-stu-id="56953-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="56953-423">Defina se um nova rede virtual e a sub-rede devem ser criados ou, deve ser utilizada uma sub-rede existente.</span><span class="sxs-lookup"><span data-stu-id="56953-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="56953-424">Se já tiver uma rede virtual que é a rede no local de tooyour ligado, selecione **existente**.</span><span class="sxs-lookup"><span data-stu-id="56953-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="56953-425">**Id de sub-rede**. Definir o ID de Olá de Olá toowhich sub-rede de Olá devem estar ligadas a máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="56953-426">Selecione a sub-rede de Olá da sua rede privada virtual (VPN) ou ExpressRoute rede virtual tooconnect Olá tooyour no local rede da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56953-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="56953-427">ID de Olá, normalmente, este aspeto:</span><span class="sxs-lookup"><span data-stu-id="56953-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="56953-428">/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} <*id de subscrição*> /resourceGroups/ <*nome do grupo de recursos*> /providers/Microsoft.Network/virtualNetworks/ <*nome da rede virtual*> /subnets/ <*nome de sub-rede*></span><span class="sxs-lookup"><span data-stu-id="56953-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="56953-429">modelo de Olá implementa uma instância de Balanceador de carga do Azure, que suporta vários sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="56953-430">instâncias ASCS Olá estão configuradas para o número da instância 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="56953-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="56953-431">instâncias SCS Olá estão configuradas para o número da instância 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="56953-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="56953-432">instâncias de servidor de replicação de colocar em fila do ASCS (ERS) (apenas Linux) Olá estão configuradas para o número da instância 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="56953-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="56953-433">instâncias do Olá SCS ERS (apenas Linux) estão configuradas para o número da instância 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="56953-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="56953-434">Olá Balanceador de carga contém 1 (2 para Linux) VIP(s), 1 x VIP para ASCS/SCS e 1 x VIP para ERS (apenas Linux).</span><span class="sxs-lookup"><span data-stu-id="56953-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="56953-435">Olá lista seguinte contém todas as regras de (em que x é o número de Olá de Olá sistema SAP, por exemplo, 1, 2, 3...) de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="56953-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="56953-436">Portas específicas do Windows para cada sistema SAP: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="56953-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="56953-437">Portas ASCS (número de instância x0): 32 x 0, 36 x 0, -39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="56953-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="56953-438">Portas SCS (número de instância x1): 32 x 1 33 x 1, 39 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="56953-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="56953-439">ASCS ERS portas no Linux (número de instância x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="56953-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="56953-440">SCS ERS portas no Linux (número de instância x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="56953-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="56953-441">Balanceador de carga Olá é Olá toouse configurado portas de pesquisa (em que x é o número de Olá de Olá sistema SAP, por exemplo, 1, 2,... 3) os seguintes:</span><span class="sxs-lookup"><span data-stu-id="56953-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="56953-442">Porta de sonda do Balanceador de carga internos ASCS/SCS: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="56953-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="56953-443">Porta da sonda (apenas Linux) do Balanceador de carga ERS internos: 621 x 2</span><span class="sxs-lookup"><span data-stu-id="56953-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="56953-444"><a name="database-template"></a>Modelo de base de dados</span><span class="sxs-lookup"><span data-stu-id="56953-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="56953-445">modelo de base de dados de Olá implementa uma ou duas máquinas virtuais que pode utilizar tooinstall Olá sistema de gestão de base de dados relacional (RDBMS) para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="56953-446">Por exemplo, se implementar um modelo ASCS/SCS para sistemas SAP cinco, terá de toodeploy este modelo de cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="56953-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="56953-447">tooset segurança Olá da base de dados várias SID modelo, Olá [modelo várias SID de base de dados] [ sap-templates-3-tier-multisid-db-marketplace-image] ou [modelo de várias SID de base de dados utilizando discos geridos] [ sap-templates-3-tier-multisid-db-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="56953-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="56953-448">**Id de sistema de SAP**. Introduza o ID de sistema SAP Olá de Olá sistema SAP pretende tooinstall.</span><span class="sxs-lookup"><span data-stu-id="56953-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="56953-449">Olá ID será utilizado como um prefixo para recursos de Olá que são implementados.</span><span class="sxs-lookup"><span data-stu-id="56953-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="56953-450">**Tipo de SO**.</span><span class="sxs-lookup"><span data-stu-id="56953-450">**Os Type**.</span></span> <span data-ttu-id="56953-451">Selecione o sistema de operativo Olá das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="56953-452">**DbType**.</span><span class="sxs-lookup"><span data-stu-id="56953-452">**Dbtype**.</span></span> <span data-ttu-id="56953-453">Selecione o tipo de Olá da base de dados de Olá pretende tooinstall no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="56953-454">Selecione **SQL** se quiser tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="56953-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="56953-455">Selecione **HANA** se máquinas de virtuais Olá planeia tooinstall SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="56953-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="56953-456">Certifique-se tooselect Olá tipo de sistema operativo correto: selecione **Windows** para SQL Server, selecione uma distribuição Linux para HANA.</span><span class="sxs-lookup"><span data-stu-id="56953-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="56953-457">Olá Balanceador de carga do Azure que está ligado toohello máquinas virtuais estejam configuradas tipo de base de dados do toosupport Olá selecionado:</span><span class="sxs-lookup"><span data-stu-id="56953-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="56953-458">**SQL SERVER**.</span><span class="sxs-lookup"><span data-stu-id="56953-458">**SQL**.</span></span> <span data-ttu-id="56953-459">Balanceador de carga Olá será a porta 1433 balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="56953-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="56953-460">Certifique-se de que toouse esta porta para a configuração do SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="56953-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="56953-461">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="56953-461">**HANA**.</span></span> <span data-ttu-id="56953-462">Balanceador de carga Olá serão as portas 35015 e 35017 de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="56953-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="56953-463">Certifique-se de que tooinstall SAP HANA com o número de instância **50**.</span><span class="sxs-lookup"><span data-stu-id="56953-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="56953-464">Balanceador de carga Olá utilizará a porta da sonda 62550.</span><span class="sxs-lookup"><span data-stu-id="56953-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="56953-465">**Tamanho do sistema de SAP**.</span><span class="sxs-lookup"><span data-stu-id="56953-465">**Sap System Size**.</span></span> <span data-ttu-id="56953-466">Número de Olá conjunto de novo sistema do SAPS Olá irá fornecer.</span><span class="sxs-lookup"><span data-stu-id="56953-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="56953-467">Se tiver a não certeza necessitará de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="56953-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="56953-468">**Disponibilidade do sistema**.</span><span class="sxs-lookup"><span data-stu-id="56953-468">**System Availability**.</span></span> <span data-ttu-id="56953-469">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="56953-469">Select **HA**.</span></span>
  -  <span data-ttu-id="56953-470">**Nome de utilizador de administrador e a palavra-passe de administrador**.</span><span class="sxs-lookup"><span data-stu-id="56953-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="56953-471">Crie um novo utilizador que pode ser utilizado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="56953-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="56953-472">**Id de sub-rede**. Introduza o ID de Olá da sub-rede Olá que utilizou durante a implementação de Olá do modelo ASCS/SCS hello, ou Olá ID de sub-rede de Olá que foi criada como parte da implementação do modelo ASCS/SCS de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="56953-473"><a name="application-servers-template"></a>Modelo de servidores de aplicações</span><span class="sxs-lookup"><span data-stu-id="56953-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="56953-474">modelo de servidores de aplicação Olá implementa dois ou mais máquinas virtuais que podem ser utilizadas como instâncias de servidor de aplicações do SAP para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="56953-475">Por exemplo, se implementar um modelo ASCS/SCS para sistemas SAP cinco, terá de toodeploy este modelo de cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="56953-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="56953-476">tooset segurança Olá servidores múltiplos SID modelo de aplicação, na Olá [modelo de SID de múltiplos servidores de aplicações] [ sap-templates-3-tier-multisid-apps-marketplace-image] ou [modelo SID de múltiplos servidores de aplicações utilizando discos geridos] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], introduza valores para Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="56953-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="56953-477">**Id de sistema de SAP**. Introduza o ID de sistema SAP Olá de Olá sistema SAP pretende tooinstall.</span><span class="sxs-lookup"><span data-stu-id="56953-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="56953-478">Olá ID será utilizado como um prefixo para recursos de Olá que são implementados.</span><span class="sxs-lookup"><span data-stu-id="56953-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="56953-479">**Tipo de SO**.</span><span class="sxs-lookup"><span data-stu-id="56953-479">**Os Type**.</span></span> <span data-ttu-id="56953-480">Selecione o sistema de operativo Olá das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="56953-481">**Tamanho do sistema de SAP**.</span><span class="sxs-lookup"><span data-stu-id="56953-481">**Sap System Size**.</span></span> <span data-ttu-id="56953-482">número de Olá de novo sistema do SAPS Olá irá fornecer.</span><span class="sxs-lookup"><span data-stu-id="56953-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="56953-483">Se tiver a não certeza necessitará de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="56953-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="56953-484">**Disponibilidade do sistema**.</span><span class="sxs-lookup"><span data-stu-id="56953-484">**System Availability**.</span></span> <span data-ttu-id="56953-485">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="56953-485">Select **HA**.</span></span>
  -  <span data-ttu-id="56953-486">**Nome de utilizador de administrador e a palavra-passe de administrador**.</span><span class="sxs-lookup"><span data-stu-id="56953-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="56953-487">Crie um novo utilizador que pode ser utilizado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="56953-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="56953-488">**Id de sub-rede**. Introduza o ID de Olá da sub-rede Olá que utilizou durante a implementação de Olá do modelo ASCS/SCS hello, ou Olá ID de sub-rede de Olá que foi criada como parte da implementação do modelo ASCS/SCS de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="56953-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="56953-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="56953-490">No nosso exemplo, o espaço de endereços de Olá de Olá rede virtual do Azure é 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="56953-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="56953-491">Há uma sub-rede denominada **sub-rede**, com um intervalo de endereços de 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="56953-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="56953-492">Todos os balanceadores de carga internos e máquinas virtuais são implementados nesta rede virtual.</span><span class="sxs-lookup"><span data-stu-id="56953-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56953-493">Não efetue as alterações toohello as definições de rede dentro Olá sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="56953-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="56953-494">Isto inclui os endereços IP, servidores DNS e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="56953-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="56953-495">Configure as definições de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="56953-496">serviço de protocolo de configuração dinâmica de anfitrião (DHCP) de Olá propaga as suas definições.</span><span class="sxs-lookup"><span data-stu-id="56953-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="56953-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Endereços IP de DNS</span><span class="sxs-lookup"><span data-stu-id="56953-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="56953-498">Olá tooset necessário que endereços IP de DNS, Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="56953-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="56953-499">No Olá portal do Azure, no Olá **servidores DNS** painel, certifique-se de que a rede virtual **servidores DNS** opção estiver definida demasiado**DNS personalizado**.</span><span class="sxs-lookup"><span data-stu-id="56953-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="56953-500">Selecione as definições com base no tipo de Olá de rede que tiver.</span><span class="sxs-lookup"><span data-stu-id="56953-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="56953-501">Para obter mais informações, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="56953-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="56953-502">[Conectividade de rede empresarial (em vários locais)][planning-guide-2.2]: adicionar endereços IP Olá dos servidores DNS Olá no local.</span><span class="sxs-lookup"><span data-stu-id="56953-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="56953-503">Pode expandir no local DNS servidores toohello máquinas virtuais que estão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="56953-504">Nesse cenário, pode adicionar endereços IP Olá de Olá Azure máquinas virtuais em que executa o serviço DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="56953-505">[Implementação apenas de nuvem][planning-guide-2.1]: implementar uma máquina virtual adicional no Olá mesma instância de rede Virtual que funciona como um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="56953-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="56953-506">Adicionar endereços de IP Olá Olá Azure máquinas virtuais que configurou toorun serviço DNS.</span><span class="sxs-lookup"><span data-stu-id="56953-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Figura 12: Configure os servidores DNS para a rede Virtual do Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="56953-508">_**Figura 12:** configurar DNS servidores para a rede Virtual do Azure_</span><span class="sxs-lookup"><span data-stu-id="56953-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="56953-509">Se alterar os endereços IP Olá dos servidores DNS Olá, terá de toorestart Olá máquinas virtuais do Azure tooapply Olá alteração e novos servidores DNS Olá de propagação.</span><span class="sxs-lookup"><span data-stu-id="56953-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="56953-510">No nosso exemplo Olá serviço DNS é instalado e configurado nestas máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="56953-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="56953-511">Função de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56953-511">Virtual machine role</span></span> | <span data-ttu-id="56953-512">Nome de anfitrião de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56953-512">Virtual machine host name</span></span> | <span data-ttu-id="56953-513">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="56953-513">Network card name</span></span> | <span data-ttu-id="56953-514">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="56953-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56953-515">Primeiro servidor de DNS</span><span class="sxs-lookup"><span data-stu-id="56953-515">First DNS server</span></span> |<span data-ttu-id="56953-516">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="56953-516">domcontr-0</span></span> |<span data-ttu-id="56953-517">PR1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="56953-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="56953-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="56953-518">10.0.0.10</span></span> |
| <span data-ttu-id="56953-519">Segundo servidor DNS</span><span class="sxs-lookup"><span data-stu-id="56953-519">Second DNS server</span></span> |<span data-ttu-id="56953-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="56953-520">domcontr-1</span></span> |<span data-ttu-id="56953-521">PR1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="56953-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="56953-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="56953-522">10.0.0.11</span></span> |

### <span data-ttu-id="56953-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nomes de anfitriões e endereços IP estáticos para a instância em cluster do SAP ASCS/SCS Olá e instância em cluster DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="56953-524">Para implementação no local, terá destes nomes de anfitrião reservado e endereços IP:</span><span class="sxs-lookup"><span data-stu-id="56953-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="56953-525">Função de nome de anfitrião virtual</span><span class="sxs-lookup"><span data-stu-id="56953-525">Virtual host name role</span></span> | <span data-ttu-id="56953-526">Nome de anfitrião virtual</span><span class="sxs-lookup"><span data-stu-id="56953-526">Virtual host name</span></span> | <span data-ttu-id="56953-527">Endereço IP estático virtual</span><span class="sxs-lookup"><span data-stu-id="56953-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56953-528">SAP ASCS/SCS primeiro cluster nome de anfitrião virtual (para gestão de cluster)</span><span class="sxs-lookup"><span data-stu-id="56953-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="56953-529">PR1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="56953-529">pr1-ascs-vir</span></span> |<span data-ttu-id="56953-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="56953-530">10.0.0.42</span></span> |
| <span data-ttu-id="56953-531">Nome de anfitrião virtual de instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="56953-532">PR1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="56953-532">pr1-ascs-sap</span></span> |<span data-ttu-id="56953-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="56953-533">10.0.0.43</span></span> |
| <span data-ttu-id="56953-534">Nome de anfitrião virtual de cluster segundo do SAP DBMS (gestão de clusters)</span><span class="sxs-lookup"><span data-stu-id="56953-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="56953-535">PR1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="56953-535">pr1-dbms-vir</span></span> |<span data-ttu-id="56953-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="56953-536">10.0.0.32</span></span> |

<span data-ttu-id="56953-537">Quando criar o cluster de Olá, criar Olá nomes de anfitrião virtual **pr1-ascs-vir** e **pr1-dbms-vir** e Olá associadas a endereços IP que gerir Olá cluster em si.</span><span class="sxs-lookup"><span data-stu-id="56953-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="56953-538">Para obter informações sobre como toodo esta, consulte [recolher nós de cluster numa configuração de cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="56953-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="56953-539">Pode criar manualmente Olá outros dois nomes de anfitrião virtual, **pr1-ascs-sap** e **pr1-dbms-sap**, e Olá associadas a endereços IP, no servidor DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="56953-540">Olá instância em cluster do SAP ASCS/SCS e Olá em cluster DBMS instância utilizar estes recursos.</span><span class="sxs-lookup"><span data-stu-id="56953-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="56953-541">Para obter informações sobre como toodo esta, consulte [criar um nome de anfitrião virtual para uma instância em cluster do SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="56953-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="56953-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de endereços IP estáticos para SAP Olá máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="56953-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="56953-543">Depois de implementar Olá toouse de máquinas virtuais do cluster, terá de endereços IP estáticos do tooset todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="56953-544">Opte por fazê-lo na configuração de rede Virtual do Azure Olá e não no sistema de operativo convidado Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="56953-545">No portal do Azure Olá, selecione **grupo de recursos** > **placa de rede** > **definições** > **endereço IP** .</span><span class="sxs-lookup"><span data-stu-id="56953-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="56953-546">No Olá **endereços IP** painel, em **atribuição**, selecione **estático**.</span><span class="sxs-lookup"><span data-stu-id="56953-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="56953-547">No Olá **endereço IP** box, introduza o endereço IP Olá que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="56953-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="56953-548">Se alterar o endereço IP Olá de placa de rede Olá, terá de toorestart Olá máquinas virtuais do Azure tooapply Olá alteração.</span><span class="sxs-lookup"><span data-stu-id="56953-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Figura 13: Conjunto de endereços IP estáticos para a placa de rede Olá de cada máquina virtual][sap-ha-guide-figure-3002]

  <span data-ttu-id="56953-550">_**Figura 13:** conjunto de endereços IP estáticos para a placa de rede Olá de cada máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="56953-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="56953-551">Repita este passo para todas as interfaces de rede, ou seja, todas as máquinas virtuais, incluindo máquinas virtuais que pretende que toouse para o seu serviço DNS/do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56953-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="56953-552">No nosso exemplo, temos destas máquinas virtuais e endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="56953-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="56953-553">Função de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56953-553">Virtual machine role</span></span> | <span data-ttu-id="56953-554">Nome de anfitrião de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56953-554">Virtual machine host name</span></span> | <span data-ttu-id="56953-555">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="56953-555">Network card name</span></span> | <span data-ttu-id="56953-556">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="56953-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56953-557">Primeira instância de servidor de aplicações SAP</span><span class="sxs-lookup"><span data-stu-id="56953-557">First SAP Application Server instance</span></span> |<span data-ttu-id="56953-558">PR1-di-0</span><span class="sxs-lookup"><span data-stu-id="56953-558">pr1-di-0</span></span> |<span data-ttu-id="56953-559">PR1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="56953-559">pr1-nic-di-0</span></span> |<span data-ttu-id="56953-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="56953-560">10.0.0.50</span></span> |
| <span data-ttu-id="56953-561">Segunda instância de servidor de aplicações SAP</span><span class="sxs-lookup"><span data-stu-id="56953-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="56953-562">PR1-di-1</span><span class="sxs-lookup"><span data-stu-id="56953-562">pr1-di-1</span></span> |<span data-ttu-id="56953-563">PR1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="56953-563">pr1-nic-di-1</span></span> |<span data-ttu-id="56953-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="56953-564">10.0.0.51</span></span> |
| <span data-ttu-id="56953-565">...</span><span class="sxs-lookup"><span data-stu-id="56953-565">...</span></span> |<span data-ttu-id="56953-566">...</span><span class="sxs-lookup"><span data-stu-id="56953-566">...</span></span> |<span data-ttu-id="56953-567">...</span><span class="sxs-lookup"><span data-stu-id="56953-567">...</span></span> |<span data-ttu-id="56953-568">...</span><span class="sxs-lookup"><span data-stu-id="56953-568">...</span></span> |
| <span data-ttu-id="56953-569">Última instância do servidor de aplicações SAP</span><span class="sxs-lookup"><span data-stu-id="56953-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="56953-570">PR1-di-5</span><span class="sxs-lookup"><span data-stu-id="56953-570">pr1-di-5</span></span> |<span data-ttu-id="56953-571">PR1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="56953-571">pr1-nic-di-5</span></span> |<span data-ttu-id="56953-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="56953-572">10.0.0.55</span></span> |
| <span data-ttu-id="56953-573">Primeiro nó de cluster para a instância ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="56953-574">PR1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="56953-574">pr1-ascs-0</span></span> |<span data-ttu-id="56953-575">PR1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="56953-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="56953-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="56953-576">10.0.0.40</span></span> |
| <span data-ttu-id="56953-577">Segundo nó de cluster para a instância ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="56953-578">PR1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="56953-578">pr1-ascs-1</span></span> |<span data-ttu-id="56953-579">PR1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="56953-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="56953-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="56953-580">10.0.0.41</span></span> |
| <span data-ttu-id="56953-581">Primeiro nó de cluster para a instância DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="56953-582">PR1-db-0</span><span class="sxs-lookup"><span data-stu-id="56953-582">pr1-db-0</span></span> |<span data-ttu-id="56953-583">PR1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="56953-583">pr1-nic-db-0</span></span> |<span data-ttu-id="56953-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="56953-584">10.0.0.30</span></span> |
| <span data-ttu-id="56953-585">Segundo nó de cluster para a instância DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="56953-586">PR1-db-1</span><span class="sxs-lookup"><span data-stu-id="56953-586">pr1-db-1</span></span> |<span data-ttu-id="56953-587">PR1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="56953-587">pr1-nic-db-1</span></span> |<span data-ttu-id="56953-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="56953-588">10.0.0.31</span></span> |

### <span data-ttu-id="56953-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Definir um endereço IP estático para o Balanceador de carga interno do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="56953-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="56953-590">modelo de SAP Azure Resource Manager Olá cria um balanceador de carga interno do Azure que é utilizado para o cluster de instância do SAP ASCS/SCS Olá e cluster DBMS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56953-591">Olá endereço IP do nome de anfitrião virtual Olá de Olá SAP ASCS/SCS é Olá mesmo como endereço IP Olá Olá Balanceador de carga interno SAP ASCS/SCS: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="56953-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="56953-592">Olá endereço IP do nome virtual Olá Olá DBMS é Olá mesmo como endereço IP Olá Olá Balanceador de carga interno DBMS: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="56953-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="56953-593">Balanceador de carga tooset um endereço IP estático para Olá Azure interno:</span><span class="sxs-lookup"><span data-stu-id="56953-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="56953-594">Olá implementação inicial define o endereço IP de Balanceador de carga interno Olá demasiado**dinâmica**.</span><span class="sxs-lookup"><span data-stu-id="56953-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="56953-595">No Olá portal do Azure, no Olá **endereços IP** painel, em **atribuição**, selecione **estático**.</span><span class="sxs-lookup"><span data-stu-id="56953-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="56953-596">Definir o endereço IP de Olá do Balanceador de carga interno Olá **pr1-lb-ascs** toohello o endereço IP do nome de anfitrião virtual Olá da instância de SAP ASCS/SCS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="56953-597">Definir o endereço IP de Olá do Balanceador de carga interno Olá **pr1-lb-dbms** toohello o endereço IP do nome de anfitrião virtual Olá da instância DBMS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Figura 14: Conjunto de endereços IP estáticos para o Balanceador de carga interno Olá para a instância de SAP ASCS/SCS Olá][sap-ha-guide-figure-3003]

  <span data-ttu-id="56953-599">_**Figura 14:** conjunto de endereços IP estáticos para o Balanceador de carga interno Olá para a instância de SAP ASCS/SCS Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="56953-600">No nosso exemplo, temos de dois balanceadores de carga internos do Azure que tenham estes endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="56953-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="56953-601">Função do Balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="56953-601">Azure internal load balancer role</span></span> | <span data-ttu-id="56953-602">Nome do Balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="56953-602">Azure internal load balancer name</span></span> | <span data-ttu-id="56953-603">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="56953-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56953-604">Balanceador de carga interno de instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="56953-605">PR1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="56953-605">pr1-lb-ascs</span></span> |<span data-ttu-id="56953-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="56953-606">10.0.0.43</span></span> |
| <span data-ttu-id="56953-607">Balanceador de carga interno SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="56953-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="56953-608">PR1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="56953-608">pr1-lb-dbms</span></span> |<span data-ttu-id="56953-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="56953-609">10.0.0.33</span></span> |


### <span data-ttu-id="56953-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga na ASCS/SCS predefinido</span><span class="sxs-lookup"><span data-stu-id="56953-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="56953-611">modelo de SAP Azure Resource Manager Olá cria portas Olá que precisa de:</span><span class="sxs-lookup"><span data-stu-id="56953-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="56953-612">Uma instância de ABAP ASCS, com o número de instância predefinido Olá **00**</span><span class="sxs-lookup"><span data-stu-id="56953-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="56953-613">Uma instância de Java SCS, com o número de instância predefinido Olá **01**</span><span class="sxs-lookup"><span data-stu-id="56953-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="56953-614">Quando instalar a instância do SAP ASCS/SCS, tem de utilizar o número de instância predefinido Olá **00** para sua ABAP ASCS instância e Olá instância número predefinido **01** para a instância do SCS de Java.</span><span class="sxs-lookup"><span data-stu-id="56953-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="56953-615">Em seguida, crie necessária pontos finais relativas às portas de SAP NetWeaver Olá de balanceamento de carga interna.</span><span class="sxs-lookup"><span data-stu-id="56953-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="56953-616">toocreate necessários pontos finais de balanceamento de carga interno, primeiro, crie estes pontos finais relativas às portas de SAP NetWeaver ABAP ASCS Olá de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="56953-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="56953-617">Nome de regra de balanceamento de carga do serviço</span><span class="sxs-lookup"><span data-stu-id="56953-617">Service/load balancing rule name</span></span> | <span data-ttu-id="56953-618">Números de porta predefinidos</span><span class="sxs-lookup"><span data-stu-id="56953-618">Default port numbers</span></span> | <span data-ttu-id="56953-619">Portas concretas para (instância ASCS com o número de instância 00) (ERS com 10)</span><span class="sxs-lookup"><span data-stu-id="56953-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56953-620">Servidor de colocar em fila / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="56953-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="56953-621">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="56953-622">3200</span><span class="sxs-lookup"><span data-stu-id="56953-622">3200</span></span> |
| <span data-ttu-id="56953-623">Servidor de mensagens ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="56953-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="56953-624">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="56953-625">3600</span><span class="sxs-lookup"><span data-stu-id="56953-625">3600</span></span> |
| <span data-ttu-id="56953-626">Mensagem ABAP interna / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="56953-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="56953-627">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="56953-628">3900</span><span class="sxs-lookup"><span data-stu-id="56953-628">3900</span></span> |
| <span data-ttu-id="56953-629">Mensagens HTTP do servidor / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="56953-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="56953-630">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="56953-631">8100</span><span class="sxs-lookup"><span data-stu-id="56953-631">8100</span></span> |
| <span data-ttu-id="56953-632">SAP iniciar serviço ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="56953-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="56953-633">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="56953-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="56953-634">50013</span><span class="sxs-lookup"><span data-stu-id="56953-634">50013</span></span> |
| <span data-ttu-id="56953-635">SAP iniciar serviço ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="56953-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="56953-636">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="56953-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="56953-637">50014</span><span class="sxs-lookup"><span data-stu-id="56953-637">50014</span></span> |
| <span data-ttu-id="56953-638">Replicação de colocar em fila / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="56953-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="56953-639">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="56953-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="56953-640">50016</span><span class="sxs-lookup"><span data-stu-id="56953-640">50016</span></span> |
| <span data-ttu-id="56953-641">HTTP de ERS de serviço de início SAP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="56953-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="56953-642">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="56953-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="56953-643">51013</span><span class="sxs-lookup"><span data-stu-id="56953-643">51013</span></span> |
| <span data-ttu-id="56953-644">HTTP de ERS de serviço de início SAP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="56953-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="56953-645">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="56953-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="56953-646">51014</span><span class="sxs-lookup"><span data-stu-id="56953-646">51014</span></span> |
| <span data-ttu-id="56953-647">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="56953-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="56953-648">5985</span><span class="sxs-lookup"><span data-stu-id="56953-648">5985</span></span> |
| <span data-ttu-id="56953-649">Partilha de ficheiros *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="56953-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="56953-650">445</span><span class="sxs-lookup"><span data-stu-id="56953-650">445</span></span> |

<span data-ttu-id="56953-651">_**Tabela 1:** porta número de instâncias de SAP NetWeaver ABAP ASCS Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="56953-652">Em seguida, crie estes pontos finais relativas às portas de SAP NetWeaver Java SCS Olá de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="56953-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="56953-653">Nome de regra de balanceamento de carga do serviço</span><span class="sxs-lookup"><span data-stu-id="56953-653">Service/load balancing rule name</span></span> | <span data-ttu-id="56953-654">Números de porta predefinidos</span><span class="sxs-lookup"><span data-stu-id="56953-654">Default port numbers</span></span> | <span data-ttu-id="56953-655">Portas concretas para (instância SCS com o número de instância 01) (ERS com 11)</span><span class="sxs-lookup"><span data-stu-id="56953-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56953-656">Servidor de colocar em fila / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="56953-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="56953-657">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="56953-658">3201</span><span class="sxs-lookup"><span data-stu-id="56953-658">3201</span></span> |
| <span data-ttu-id="56953-659">Servidor de gateway / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="56953-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="56953-660">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="56953-661">3301</span><span class="sxs-lookup"><span data-stu-id="56953-661">3301</span></span> |
| <span data-ttu-id="56953-662">Servidor de mensagens de Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="56953-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="56953-663">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="56953-664">3901</span><span class="sxs-lookup"><span data-stu-id="56953-664">3901</span></span> |
| <span data-ttu-id="56953-665">Mensagens HTTP do servidor / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="56953-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="56953-666">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="56953-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="56953-667">8101</span><span class="sxs-lookup"><span data-stu-id="56953-667">8101</span></span> |
| <span data-ttu-id="56953-668">SAP iniciar serviço SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="56953-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="56953-669">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="56953-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="56953-670">50113</span><span class="sxs-lookup"><span data-stu-id="56953-670">50113</span></span> |
| <span data-ttu-id="56953-671">SAP iniciar serviço SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="56953-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="56953-672">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="56953-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="56953-673">50114</span><span class="sxs-lookup"><span data-stu-id="56953-673">50114</span></span> |
| <span data-ttu-id="56953-674">Replicação de colocar em fila / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="56953-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="56953-675">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="56953-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="56953-676">50116</span><span class="sxs-lookup"><span data-stu-id="56953-676">50116</span></span> |
| <span data-ttu-id="56953-677">HTTP de ERS de serviço de início SAP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="56953-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="56953-678">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="56953-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="56953-679">51113</span><span class="sxs-lookup"><span data-stu-id="56953-679">51113</span></span> |
| <span data-ttu-id="56953-680">HTTP de ERS de serviço de início SAP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="56953-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="56953-681">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="56953-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="56953-682">51114</span><span class="sxs-lookup"><span data-stu-id="56953-682">51114</span></span> |
| <span data-ttu-id="56953-683">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="56953-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="56953-684">5985</span><span class="sxs-lookup"><span data-stu-id="56953-684">5985</span></span> |
| <span data-ttu-id="56953-685">Partilha de ficheiros *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="56953-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="56953-686">445</span><span class="sxs-lookup"><span data-stu-id="56953-686">445</span></span> |

<span data-ttu-id="56953-687">_**Tabela 2:** porta número de instâncias de SAP NetWeaver Java SCS Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga na predefinição ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="56953-689">_**Figura 15:** regras para o Balanceador de carga interno do Azure Olá de balanceamento de carga de predefinição ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="56953-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="56953-690">Definir o endereço IP Olá Olá de Balanceador de carga **pr1-lb-dbms** toohello o endereço IP do nome de anfitrião virtual Olá da instância DBMS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="56953-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Altere as regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do Olá ASCS/SCS predefinido</span><span class="sxs-lookup"><span data-stu-id="56953-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="56953-692">Se quiser toouse diferentes números de Olá SAP ASCS ou instâncias SCS, tem de alterar os nomes de Olá e valores das suas portas de valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="56953-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="56953-693">No portal do Azure Olá, selecione  **<* SID*> - lb - ascs carregar balanceador * * > **regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="56953-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="56953-694">Todas as regras que pertencem toohello SAP ASCS ou uma instância de SCS de balanceamento de carga, altere estes valores:</span><span class="sxs-lookup"><span data-stu-id="56953-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="56953-695">Nome</span><span class="sxs-lookup"><span data-stu-id="56953-695">Name</span></span>
  * <span data-ttu-id="56953-696">Porta</span><span class="sxs-lookup"><span data-stu-id="56953-696">Port</span></span>
  * <span data-ttu-id="56953-697">Porta de back-end</span><span class="sxs-lookup"><span data-stu-id="56953-697">Back-end port</span></span>

  <span data-ttu-id="56953-698">Por exemplo, se pretender que o número de instância do toochange Olá predefinido ASCS de 00 too31, terá das alterações de Olá toomake para todas as portas listadas na tabela 1.</span><span class="sxs-lookup"><span data-stu-id="56953-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="56953-699">Eis um exemplo de uma atualização para a porta *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="56953-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Alterar as regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do Olá ASCS/SCS predefinido][sap-ha-guide-figure-3005]

  <span data-ttu-id="56953-701">_**Figura 16:** alteração Olá ASCS/SCS predefinido balanceamento de carga regras Olá Azure interno Balanceador de carga_</span><span class="sxs-lookup"><span data-stu-id="56953-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="56953-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Adicionar o domínio de toohello de máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="56953-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="56953-703">Depois de atribuir um endereço IP estático máquinas de virtuais de toohello, adicione domínio de toohello Olá máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Figura 17: Adicionar um domínio de tooa de máquina virtual][sap-ha-guide-figure-3006]

<span data-ttu-id="56953-705">_**Figura 17:** adicionar um domínio de tooa de máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="56953-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="56953-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Adicionar entradas de registo em ambos os nós de cluster de instância de SAP ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="56953-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="56953-707">Balanceador de carga do Azure tem um balanceador de carga interno que fechar ligações quando ligações Olá estão Inativas, defina durante um período de tempo (um tempo limite de inatividade).</span><span class="sxs-lookup"><span data-stu-id="56953-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="56953-708">Os processos de trabalho do SAP na caixa de diálogo instâncias abrir ligações toohello SAP colocar em fila processam assim Olá primeiro colocar em fila/anular pedido toobe necessidades, enviada.</span><span class="sxs-lookup"><span data-stu-id="56953-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="56953-709">Estas ligações normalmente permanecem estabelecidas até que o processo de trabalho de Olá ou Olá colocar em fila processo reinicia.</span><span class="sxs-lookup"><span data-stu-id="56953-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="56953-710">No entanto, se Olá estiver inativa durante um período de tempo definido, Olá ligações de Olá de fechar de Balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="56953-711">Esta operação não é um problema porque Olá processo de trabalho SAP reestablishes o processo de colocar em fila Olá ligação toohello se já não existe.</span><span class="sxs-lookup"><span data-stu-id="56953-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="56953-712">Estas atividades estão documentadas em rastreios de programador Olá dos processos SAP, mas que crie uma grande quantidade de conteúdo adicional nesses rastreios.</span><span class="sxs-lookup"><span data-stu-id="56953-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="56953-713">É Olá de toochange uma boa ideia TCP/IP `KeepAliveTime` e `KeepAliveInterval` em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="56953-714">Combine estas alterações nos parâmetros de TCP/IP Olá com parâmetros de perfil do SAP, descritos mais à frente artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="56953-715">entradas do registo tooadd em ambos os nós de cluster de instância do SAP ASCS/SCS Olá, primeiro, adicione estas entradas de registo do Windows em ambos os nós de cluster do Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="56953-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="56953-716">Caminho</span><span class="sxs-lookup"><span data-stu-id="56953-716">Path</span></span> | <span data-ttu-id="56953-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="56953-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="56953-718">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="56953-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="56953-719">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="56953-719">Variable type</span></span> |<span data-ttu-id="56953-720">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="56953-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="56953-721">Valor</span><span class="sxs-lookup"><span data-stu-id="56953-721">Value</span></span> |<span data-ttu-id="56953-722">120000</span><span class="sxs-lookup"><span data-stu-id="56953-722">120000</span></span> |
| <span data-ttu-id="56953-723">Ligação toodocumentation</span><span class="sxs-lookup"><span data-stu-id="56953-723">Link toodocumentation</span></span> |[<span data-ttu-id="56953-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="56953-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="56953-725">_**Tabela 3:** alteração Olá primeiro TCP/IP parâmetro_</span><span class="sxs-lookup"><span data-stu-id="56953-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="56953-726">Em seguida, adicione este entradas de registo do Windows em ambos os nós de cluster do Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="56953-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="56953-727">Caminho</span><span class="sxs-lookup"><span data-stu-id="56953-727">Path</span></span> | <span data-ttu-id="56953-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="56953-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="56953-729">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="56953-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="56953-730">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="56953-730">Variable type</span></span> |<span data-ttu-id="56953-731">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="56953-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="56953-732">Valor</span><span class="sxs-lookup"><span data-stu-id="56953-732">Value</span></span> |<span data-ttu-id="56953-733">120000</span><span class="sxs-lookup"><span data-stu-id="56953-733">120000</span></span> |
| <span data-ttu-id="56953-734">Ligação toodocumentation</span><span class="sxs-lookup"><span data-stu-id="56953-734">Link toodocumentation</span></span> |[<span data-ttu-id="56953-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="56953-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="56953-736">_**Tabela 4:** alteração Olá segundo TCP/IP parâmetro_</span><span class="sxs-lookup"><span data-stu-id="56953-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="56953-737">**alterações de Olá tooapply, reinicie ambos os nós de cluster**.</span><span class="sxs-lookup"><span data-stu-id="56953-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="56953-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Configurar um cluster de Clustering de ativação pós-falha do Windows Server para uma instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="56953-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="56953-739">Configurar um cluster de Clustering de ativação pós-falha do Windows Server para uma instância do SAP ASCS/SCS envolve estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="56953-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="56953-740">Recolha de nós de cluster Olá numa configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="56953-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="56953-741">Configurar um testemunho de partilha de ficheiros do cluster</span><span class="sxs-lookup"><span data-stu-id="56953-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="56953-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Recolher nós de cluster Olá numa configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="56953-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="56953-743">Olá adicionar funções e funcionalidades do assistente, adicione tooboth nós de cluster de clustering de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="56953-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="56953-744">Configure o cluster de ativação pós-falha de Olá utilizando o Gestor de clusters de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="56953-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="56953-745">No Gestor de clusters de ativação pós-falha, selecione **criar Cluster**e, em seguida, adicione apenas Olá nome de cluster de primeiro Olá, a nó. Não adicionar o Olá segundo nó ainda; irá adicionar o segundo nó de Olá num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="56953-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Figura 18: Adicionar servidor Olá ou nome de máquina virtual do nó do cluster primeiro Olá][sap-ha-guide-figure-3007]

  <span data-ttu-id="56953-747">_**Figura 18:** adicionar Olá servidor ou máquina virtual o nome do nó do cluster primeiro Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="56953-748">Introduza o nome de rede Olá (nome de anfitrião virtual) do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Figura 19: Introduza o nome do cluster Olá][sap-ha-guide-figure-3008]

  <span data-ttu-id="56953-750">_**Figura 19:** introduza o nome de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="56953-751">Depois de criar o cluster de Olá, execute um teste de validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Figura 20: Executar a verificação de validação de cluster de Olá][sap-ha-guide-figure-3009]

  <span data-ttu-id="56953-753">_**Figura 20:** executar verificação de validação de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="56953-754">Pode ignorar quaisquer avisos sobre discos neste momento no processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="56953-755">Irá adicionar que um testemunho de partilha de ficheiros e Olá SIOS discos partilhados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="56953-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="56953-756">Nesta fase, não precisa de tooworry relacionada com um quórum.</span><span class="sxs-lookup"><span data-stu-id="56953-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Figura 21: For encontrado nenhum disco de quórum][sap-ha-guide-figure-3010]

  <span data-ttu-id="56953-758">_**Figura 21:** não for encontrado nenhum disco de quórum_</span><span class="sxs-lookup"><span data-stu-id="56953-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: Recurso de cluster Core necessita de um novo endereço IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="56953-760">_**Figura 22:** recurso de cluster Core necessita de um novo endereço IP_</span><span class="sxs-lookup"><span data-stu-id="56953-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="56953-761">Alterar o endereço IP Olá Olá principal de serviço de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="56953-762">cluster de Olá não é possível iniciar até alterar o endereço IP Olá Olá principal de serviço de cluster, porque o endereço IP de hello do servidor de Olá pontos tooone de nós de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="56953-763">Fazê-lo no Olá **propriedades** página do recurso de IP do serviço de Olá core cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="56953-764">Por exemplo, é necessário um endereço IP de tooassign (no nosso exemplo, **10.0.0.42**) para o nome de anfitrião virtual de cluster Olá **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="56953-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: Na caixa de diálogo de propriedades de Olá, alterar o endereço IP Olá][sap-ha-guide-figure-3012]

  <span data-ttu-id="56953-766">_**Figura 23:** no Olá **propriedades** caixa de diálogo, o endereço IP de Olá de alteração_</span><span class="sxs-lookup"><span data-stu-id="56953-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Figura 24: Atribuir o endereço IP de Olá que está reservado para o cluster de Olá][sap-ha-guide-figure-3013]

  <span data-ttu-id="56953-768">_**Figura 24:** atribuir o endereço IP Olá que está reservado para o cluster de Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="56953-769">Coloque o nome de anfitrião virtual de cluster de Olá online.</span><span class="sxs-lookup"><span data-stu-id="56953-769">Bring hello cluster virtual host name online.</span></span>

  ![Figura 25: O serviço de núcleo de Cluster está operacional e em execução e com Olá corrija o endereço IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="56953-771">_**Figura 25:** serviço de núcleo de Cluster está operacional e em execução e com Olá corrija o endereço IP_</span><span class="sxs-lookup"><span data-stu-id="56953-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="56953-772">Adicione Olá segundo nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="56953-773">Agora que o serviço de cluster de núcleos de Olá está a funcionar, pode adicionar o segundo nó de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Figura 26: Adicionar Olá segundo o nó de cluster][sap-ha-guide-figure-3015]

  <span data-ttu-id="56953-775">_**Figura 26:** adicionar Olá segundo cluster nó_</span><span class="sxs-lookup"><span data-stu-id="56953-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="56953-776">Introduza um nome de anfitrião do nó de cluster Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="56953-776">Enter a name for hello second cluster node host.</span></span>

  ![Figura 27: Introduza o nome de anfitrião de nó Olá segundo cluster][sap-ha-guide-figure-3016]

  <span data-ttu-id="56953-778">_**Figura 27:** Enter Olá segundo cluster nó nome de anfitrião_</span><span class="sxs-lookup"><span data-stu-id="56953-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="56953-779">Se possível esse Olá **adicionar todos os clusters de toohello o armazenamento elegível** caixa de verificação está **não** selecionado.</span><span class="sxs-lookup"><span data-stu-id="56953-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: Não selecione a caixa de verificação Olá][sap-ha-guide-figure-3017]

  <span data-ttu-id="56953-781">_**Figura 28:** fazer **não** Olá, selecione a caixa de verificação_</span><span class="sxs-lookup"><span data-stu-id="56953-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="56953-782">Pode ignorar avisos sobre o quórum e de discos.</span><span class="sxs-lookup"><span data-stu-id="56953-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="56953-783">Iremos definir disco de Olá quórum e partilha hello mais tarde, conforme descrito em [instalar SIOS DataKeeper Cluster Edition para partilha de disco em cluster SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="56953-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorar avisos sobre o quórum de disco Olá][sap-ha-guide-figure-3018]

  <span data-ttu-id="56953-785">_**Figura 29:** ignorar avisos sobre o quórum de disco Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="56953-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Configurar um testemunho de partilha de ficheiros do cluster</span><span class="sxs-lookup"><span data-stu-id="56953-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="56953-787">Configurar um testemunho de partilha de ficheiros do cluster envolve estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="56953-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="56953-788">Criar uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="56953-788">Creating a file share</span></span>
- <span data-ttu-id="56953-789">A definição de quórum de testemunho de partilha de ficheiros de Olá no Gestor de clusters de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="56953-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="56953-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Criar uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="56953-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="56953-791">Selecione um testemunho de partilha de ficheiros em vez de um disco de quórum.</span><span class="sxs-lookup"><span data-stu-id="56953-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="56953-792">SIOS DataKeeper suportar esta opção.</span><span class="sxs-lookup"><span data-stu-id="56953-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="56953-793">Nos exemplos de Olá neste artigo, Olá testemunho de partilha de ficheiros está num servidor DNS/do Active Directory de Olá que está em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="56953-794">Olá testemunho de partilha de ficheiro é denominado **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="56953-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="56953-795">Porque iria configurou um tooAzure de ligação VPN (através de VPN de Site para Site ou Azure ExpressRoute), o DNS do Active Directory/serviço é no local e não é um ficheiro de toorun adequado testemunho de partilha.</span><span class="sxs-lookup"><span data-stu-id="56953-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="56953-796">Se o serviço DNS/do Active Directory é executado apenas no local, não configure o testemunho de partilha de ficheiros no sistema de operativo de Active Directory/DNS Windows hello que está a ser executado no local.</span><span class="sxs-lookup"><span data-stu-id="56953-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="56953-797">Latência de rede entre nós de cluster em execução no Azure e o DNS/do Active Directory no local poderá ser demasiado grande e causar problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="56953-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="56953-798">Ser se tooconfigure Olá testemunho de partilha ficheiros numa máquina virtual do Azure que está a executar o nó de cluster toohello fechar.</span><span class="sxs-lookup"><span data-stu-id="56953-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="56953-799">unidade de quórum Olá necessita de, pelo menos, 1.024 MB de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="56953-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="56953-800">Recomendamos 2.048 MB de espaço livre de disco de quórum Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="56953-801">Adicione o objeto de nome de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-801">Add hello cluster name object.</span></span>

  ![Figura 30: Atribua permissões de Olá numa partilha de Olá para o objeto de nome de cluster Olá][sap-ha-guide-figure-3019]

  <span data-ttu-id="56953-803">_**Figura 30:** atribuir permissões de Olá numa partilha de Olá para o objeto de nome de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="56953-804">Certifique-se de que as permissões de Olá incluem dados de toochange de autoridade de Olá numa partilha de Olá para o objeto de nome de cluster Olá (no nosso exemplo, **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="56953-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="56953-805">tooadd Olá cluster nome objeto toohello lista, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="56953-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="56953-806">Alterar o filtro de Olá toocheck para objetos de computador, no toothose adição mostrado na figura 31.</span><span class="sxs-lookup"><span data-stu-id="56953-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Figura 31: Alterar computadores de tooinclude Olá tipos de objeto][sap-ha-guide-figure-3020]

  <span data-ttu-id="56953-808">_**Figura 31:** alterar computadores de tooinclude Olá tipos de objeto_</span><span class="sxs-lookup"><span data-stu-id="56953-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![Figura 32: Selecione a caixa de verificação de computadores de Olá][sap-ha-guide-figure-3021]

  <span data-ttu-id="56953-810">_**Figura 32:** Olá selecione **computadores** caixa de verificação_</span><span class="sxs-lookup"><span data-stu-id="56953-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="56953-811">Introduza o objeto de nome de cluster Olá conforme mostrado na figura 31.</span><span class="sxs-lookup"><span data-stu-id="56953-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="56953-812">Porque o registo de Olá já tiver sido criado, pode alterar as permissões de Olá, conforme mostrado na figura 30.</span><span class="sxs-lookup"><span data-stu-id="56953-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="56953-813">Selecione Olá **segurança** separador da partilha de Olá e, em seguida, defina mais detalhadas permissões para o objeto de nome de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Figura 33: Definir atributos de segurança de Olá do objeto de nome de cluster Olá no quórum de partilha de ficheiros de Olá][sap-ha-guide-figure-3022]

  <span data-ttu-id="56953-815">_**Figura 33:** definir atributos de segurança de Olá do objeto de nome de cluster Olá no quórum de partilha de ficheiros de Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="56953-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Definir quórum de testemunho de partilha de ficheiros de Olá no Gestor de clusters de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="56953-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="56953-817">Abra Olá Assistente de definição de quórum de configurar.</span><span class="sxs-lookup"><span data-stu-id="56953-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Iniciar Olá Assistente de definição de quórum de Cluster de configurar][sap-ha-guide-figure-3023]

  <span data-ttu-id="56953-819">_**Figura 34:** início Olá configurar Assistente de definição de quórum de Cluster_</span><span class="sxs-lookup"><span data-stu-id="56953-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="56953-820">No Olá **selecione configuração do quórum** página, selecione **selecionar testemunho de quórum Olá**.</span><span class="sxs-lookup"><span data-stu-id="56953-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![35 figura: Pode escolher entre configurações de quórum][sap-ha-guide-figure-3024]

  <span data-ttu-id="56953-822">_**Figura 35:** configurações de quórum, pode escolher entre_</span><span class="sxs-lookup"><span data-stu-id="56953-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="56953-823">No Olá **selecionar testemunho de quórum** página, selecione **configurar um testemunho de partilha de ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="56953-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figura 36: Testemunho de partilha de ficheiros de Olá selecione][sap-ha-guide-figure-3025]

  <span data-ttu-id="56953-825">_**Figura 36:** selecione Olá testemunho de partilha de ficheiros_</span><span class="sxs-lookup"><span data-stu-id="56953-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="56953-826">Introduza a partilha de ficheiros de toohello de caminho UNC Olá (no nosso exemplo, \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="56953-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="56953-827">uma lista de alterações de Olá que pode fazer, selecione de toosee **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="56953-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Figura 37: Definir localização de partilha de ficheiros de Olá para partilha de testemunho Olá][sap-ha-guide-figure-3026]

  <span data-ttu-id="56953-829">_**Figura 37:** Definir localização de partilha de ficheiros de Olá para partilha de testemunho Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="56953-830">Selecione as alterações de Olá que pretende e, em seguida, selecione **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="56953-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="56953-831">Terá de toosuccessfully reconfigurar a configuração de cluster Olá conforme mostrado na figura 38.</span><span class="sxs-lookup"><span data-stu-id="56953-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![38 figura: Se tiver reconfigurado cluster Olá de confirmação][sap-ha-guide-figure-3027]

  <span data-ttu-id="56953-833">_**Figura 38:** confirmação que tiver reconfigurado cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="56953-834">Depois de instalar com êxito Olá Cluster de ativação pós-falha do Windows, as alterações precisam de toobe efetuada tooconditions de deteção de ativação pós-falha do toosome limiares tooadapt no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="56953-835">Olá toobe parâmetros alterado estão documentados neste blogue: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="56953-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="56953-836">Partindo do princípio de que as duas VMs que criar Olá configuração de Cluster do Windows para ASCS/SCS na estão Olá mesma sub-rede, hello parâmetros seguintes necessário toobe alterado toothese valores:</span><span class="sxs-lookup"><span data-stu-id="56953-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="56953-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="56953-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="56953-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="56953-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="56953-839">Estas definições foram testadas com os clientes e fornecidas toobe um compromisso boa resiliente suficiente no lado Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="56953-840">No Olá por outro lado essas definições foram fornecer rápido suficiente ativação pós-falha em condições de erro real em caso de falha SAP, software ou o nó/VM.</span><span class="sxs-lookup"><span data-stu-id="56953-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="56953-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar SIOS DataKeeper Cluster Edition para partilha de disco de cluster em SAP ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="56953-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="56953-842">Agora tem uma configuração de Clustering de ativação pós-falha do Windows Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="56953-843">No entanto, tooinstall uma instância do SAP ASCS/SCS, precisa de um recurso de disco partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="56953-844">Não é possível criar recursos de disco Olá partilhado que terá no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="56953-845">SIOS DataKeeper Cluster Edition é uma solução de terceiros podem utilizar recursos de disco toocreate partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="56953-846">Instalar SIOS DataKeeper Cluster Edition para Olá SAP ASCS/SCS partilha de disco em cluster envolve estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="56953-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="56953-847">Adicionar Olá .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="56953-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="56953-848">Instalar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="56953-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="56953-849">Configurar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="56953-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="56953-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Adicionar Olá .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="56953-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="56953-851">Olá o Microsoft .NET Framework 3.5 automaticamente não está ativado ou não está instalado no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="56953-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="56953-852">Uma vez SIOS DataKeeper requer Olá toobe de .NET Framework em todos os nós que instala DataKeeper no, tem de instalar Olá .NET Framework 3.5 no sistema de operativo convidado Olá de todas as máquinas virtuais no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="56953-853">Existem Olá duas formas de tooadd .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="56953-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="56953-854">Utilize o assistente Olá adicionar funções e funcionalidades no Windows conforme mostrado na figura 39.</span><span class="sxs-lookup"><span data-stu-id="56953-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Instalar Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades][sap-ha-guide-figure-3028]

  <span data-ttu-id="56953-856">_**Figura 39:** Olá de instalação do .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades_</span><span class="sxs-lookup"><span data-stu-id="56953-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Figura 40: Progresso da instalação de barra quando instala Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades][sap-ha-guide-figure-3029]

  <span data-ttu-id="56953-858">_**Figura 40:** progresso da instalação de barra quando instala Olá .NET Framework 3.5 utilizando o assistente Olá adicionar funções e funcionalidades_</span><span class="sxs-lookup"><span data-stu-id="56953-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="56953-859">Utilize Olá ferramenta da linha de comandos dism.exe.</span><span class="sxs-lookup"><span data-stu-id="56953-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="56953-860">Para este tipo de instalação, terá de diretório de SxS Olá tooaccess no Olá suporte de instalação do Windows.</span><span class="sxs-lookup"><span data-stu-id="56953-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="56953-861">Na linha de comandos elevada, escreva:</span><span class="sxs-lookup"><span data-stu-id="56953-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="56953-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>Instalar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="56953-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="56953-863">Instale SIOS DataKeeper Cluster Edition em cada nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="56953-864">toocreate virtual armazenamento partilhado com SIOS DataKeeper, crie um espelho sincronizado e, em seguida, simular o armazenamento partilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="56953-865">Antes de instalar o software SIOS Olá, criar utilizador de domínio Olá **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="56953-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-866">Adicionar Olá **DataKeeperSvc** utilizador toohello **Administrador Local** grupo em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="56953-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="56953-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="56953-868">Instale o software SIOS Olá em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![Instalador SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Primeira página do Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3031]

  <span data-ttu-id="56953-871">_**Figura 41:** primeira página do Olá SIOS DataKeeper instalação_</span><span class="sxs-lookup"><span data-stu-id="56953-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="56953-872">Na caixa de diálogo de Olá mostrada na figura 42, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="56953-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: DataKeeper informa-o se um serviço será desativado][sap-ha-guide-figure-3032]

  <span data-ttu-id="56953-874">_**Figura 42:** DataKeeper informa que um serviço vai ser desativado_</span><span class="sxs-lookup"><span data-stu-id="56953-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="56953-875">Na caixa de diálogo de Olá mostrada na figura 43, recomendamos que selecione **conta de domínio ou servidor**.</span><span class="sxs-lookup"><span data-stu-id="56953-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Seleção de utilizador para SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="56953-877">_**Figura 43:** seleção do utilizador para SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="56953-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="56953-878">Introduza o nome de utilizador da conta de domínio de Olá e palavras-passe que criou para SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="56953-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Introduza o nome de utilizador de domínio Olá e a palavra-passe para Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3034]

  <span data-ttu-id="56953-880">_**Figura 44:** introduza o nome de utilizador de domínio Olá e a palavra-passe para Olá SIOS DataKeeper instalação_</span><span class="sxs-lookup"><span data-stu-id="56953-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="56953-881">Instale a chave de licença de Olá na sua instância SIOS DataKeeper conforme mostrado na figura 45.</span><span class="sxs-lookup"><span data-stu-id="56953-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: Introduza a chave de licença de SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="56953-883">_**Figura 45:** introduzir a chave de licença SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="56953-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="56953-884">Quando lhe for pedido, reinicie a máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="56953-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>Configurar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="56953-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="56953-886">Depois de instalar SIOS DataKeeper em ambos os nós, terá de configuração de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="56953-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="56953-887">objetivo Olá configuração Olá é a replicação de dados síncrona toohave entre discos adicionais Olá ligado tooeach das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="56953-888">Iniciar Olá DataKeeper gestão e a ferramenta de configuração e, em seguida, selecione **ligar servidor**.</span><span class="sxs-lookup"><span data-stu-id="56953-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="56953-889">(Na figura 46, esta opção está dentro de um círculo vermelho.)</span><span class="sxs-lookup"><span data-stu-id="56953-889">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Ferramenta de configuração e SIOS DataKeeper gestão][sap-ha-guide-figure-3036]

  <span data-ttu-id="56953-891">_**Figura 46:** ferramenta SIOS DataKeeper gestão e configuração_</span><span class="sxs-lookup"><span data-stu-id="56953-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="56953-892">Introduza Olá nome ou endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e, um segundo passo, o segundo nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Figura 47: Nome de Olá de inserção ou o endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e um segundo passo, o segundo nó de Olá][sap-ha-guide-figure-3037]

  <span data-ttu-id="56953-894">_**Figura 47:** nome Olá de inserção ou endereço de TCP/IP Olá primeiro nó Olá gestão e configuração da ferramenta de deve ligar e um segundo passo, o segundo nó de Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="56953-895">Crie tarefa de replicação de Olá entre dois nós de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-895">Create hello replication job between hello two nodes.</span></span>

  ![Figura 48: Criar uma tarefa de replicação][sap-ha-guide-figure-3038]

  <span data-ttu-id="56953-897">_**Figura 48:** criar uma tarefa de replicação_</span><span class="sxs-lookup"><span data-stu-id="56953-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="56953-898">Um assistente orienta-o processo de Olá de criação de uma tarefa de replicação.</span><span class="sxs-lookup"><span data-stu-id="56953-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="56953-899">Defina nome Olá, o endereço de TCP/IP e o volume do disco do nó de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Figura 49: Definir o nome de Olá da tarefa de replicação de Olá][sap-ha-guide-figure-3039]

  <span data-ttu-id="56953-901">_**Figura 49:** definir o nome de Olá da tarefa de replicação de Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Figura 50: Definir a base de dados de Olá para o nó de Olá, que deve ser o nó de origem atual Olá][sap-ha-guide-figure-3040]

  <span data-ttu-id="56953-903">_**Figura 50:** definir Olá base de dados para o nó de Olá, que deve ser o nó de origem atual Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="56953-904">Defina nome Olá, o endereço de TCP/IP e o volume de disco do nó de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Figura 51: Definir os dados de base de Olá para o nó de Olá, que deve ser o nó de destino atual Olá][sap-ha-guide-figure-3041]

  <span data-ttu-id="56953-906">_**Figura 51:** definir Olá base de dados para o nó de Olá, que deve ser o nó de destino atual Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="56953-907">Defina os algoritmos de compressão Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-907">Define hello compression algorithms.</span></span> <span data-ttu-id="56953-908">No nosso exemplo, recomendamos que comprimir o fluxo de replicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="56953-909">Especialmente em situações de ressincronização, Olá a compressão de fluxo de replicação de Olá reduz significativamente o tempo de ressincronização.</span><span class="sxs-lookup"><span data-stu-id="56953-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="56953-910">Tenha em atenção que a compressão utiliza recursos de CPU e RAM Olá de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56953-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="56953-911">À medida que aumenta a taxa de compressão Olá, por isso, Olá volume dos recursos de CPU utilizado.</span><span class="sxs-lookup"><span data-stu-id="56953-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="56953-912">Também pode ajustar esta definição mais tarde.</span><span class="sxs-lookup"><span data-stu-id="56953-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="56953-913">Precisa de outra definição toocheck é se ocorre a replicação de Olá assíncrona ou síncrona.</span><span class="sxs-lookup"><span data-stu-id="56953-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="56953-914">*Quando protege configurações de SAP ASCS/SCS, tem de utilizar replicação síncrona*.</span><span class="sxs-lookup"><span data-stu-id="56953-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definir os detalhes de replicação][sap-ha-guide-figure-3042]

  <span data-ttu-id="56953-916">_**Figura 52:** definir os detalhes de replicação_</span><span class="sxs-lookup"><span data-stu-id="56953-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="56953-917">Defina se o volume de Olá que é replicado pela tarefa de replicação de Olá deve ser representado tooa configuração de cluster Clustering de ativação pós-falha do Windows Server como um disco partilhado.</span><span class="sxs-lookup"><span data-stu-id="56953-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="56953-918">Para a configuração de SAP ASCS/SCS Olá, selecione **Sim** para que o Windows hello cluster vê Olá volume replicada como um disco partilhado que possa utilizar como um volume de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Selecione Sim tooset Olá replicado volume como volume de cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="56953-920">_**Figura 53:** selecione **Sim** tooset Olá replicado volume como um volume de cluster_</span><span class="sxs-lookup"><span data-stu-id="56953-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="56953-921">Após a criação do volume de Olá, a ferramenta de configuração e gestão DataKeeper Olá mostra que a tarefa de replicação Olá está ativa.</span><span class="sxs-lookup"><span data-stu-id="56953-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Figura 54 em que: DataKeeper espelhamento síncrono de Olá SAP ASCS/SCS partilha de disco está ativo][sap-ha-guide-figure-3044]

  <span data-ttu-id="56953-923">_**Figura 54 em que:** DataKeeper espelhamento síncrono para hello SAP ASCS/SCS partilhar disco está ativo_</span><span class="sxs-lookup"><span data-stu-id="56953-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="56953-924">Gestor de clusters de ativação pós-falha mostra agora disco Olá como um disco de DataKeeper, conforme mostrado na figura 55.</span><span class="sxs-lookup"><span data-stu-id="56953-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: O Gestor de clusters de ativação pós-falha mostra disco Olá que foram replicada para DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="56953-926">_**Figura 55:** Gestor de clusters de ativação pós-falha mostra disco Olá esse DataKeeper replicado_</span><span class="sxs-lookup"><span data-stu-id="56953-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="56953-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar o sistema de SAP NetWeaver Olá</span><span class="sxs-lookup"><span data-stu-id="56953-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="56953-928">Iremos não descrevem o programa de configuração do Olá DBMS porque setups variam consoante Olá sistema DBMS que utiliza.</span><span class="sxs-lookup"><span data-stu-id="56953-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="56953-929">No entanto, partimos do princípio que preocupações de elevada disponibilidade com Olá DBMS são tratadas com funcionalidades de Olá fornecedores DBMS diferentes Olá suportem do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="56953-930">Por exemplo, Always On ou espelhamento de base de dados para o SQL Server e Oracle Data Guard para bases de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="56953-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="56953-931">Cenário de Olá que utilizamos neste artigo, iremos não adicionar mais proteção toohello DBMS.</span><span class="sxs-lookup"><span data-stu-id="56953-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="56953-932">Não existem não existem considerações especiais quando os diferentes serviços DBMS interagem com este tipo de configuração em cluster do SAP ASCS/SCS no Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-933">procedimentos de instalação de Olá do SAP NetWeaver ABAP sistemas, sistemas de Java e sistemas ABAP + Java são quase idênticos.</span><span class="sxs-lookup"><span data-stu-id="56953-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="56953-934">diferença mais significativa Olá é que um sistema de SAP ABAP tem uma instância ASCS.</span><span class="sxs-lookup"><span data-stu-id="56953-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="56953-935">Olá sistema SAP Java tem uma instância SCS.</span><span class="sxs-lookup"><span data-stu-id="56953-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="56953-936">Olá sistema SAP ABAP + Java tem uma instância ASCS e Olá de uma instância SCS em execução no mesmo grupo de cluster de ativação pós-falha da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="56953-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="56953-937">Todas as diferenças de instalação para cada pilha de instalação do SAP NetWeaver explicitamente são mencionadas.</span><span class="sxs-lookup"><span data-stu-id="56953-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="56953-938">Pode assumir que são Olá todas as outras partes do mesmo.</span><span class="sxs-lookup"><span data-stu-id="56953-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="56953-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Instale o SAP com uma instância ASCS/SCS de elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="56953-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56953-940">Certifique-se de não tooplace sua página de ficheiros no DataKeeper espelhada volumes.</span><span class="sxs-lookup"><span data-stu-id="56953-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="56953-941">DataKeeper não suporta volumes espelhados.</span><span class="sxs-lookup"><span data-stu-id="56953-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="56953-942">Pode deixar o ficheiro de paginação na unidade temporária Olá D de uma máquina virtual do Azure, que é Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="56953-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="56953-943">Se este não estiver lá, mova Olá Windows página ficheiro toodrive d: da sua máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="56953-944">Instalação do SAP com uma instância ASCS/SCS de elevada disponibilidade envolve estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="56953-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="56953-945">Criar um nome de anfitrião virtual para a instância de SAP ASCS/SCS Olá em cluster</span><span class="sxs-lookup"><span data-stu-id="56953-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="56953-946">Instalar Olá SAP primeiro nó de cluster</span><span class="sxs-lookup"><span data-stu-id="56953-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="56953-947">Modificar o perfil SAP Olá da instância ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="56953-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="56953-948">Adicionar uma porta de pesquisa</span><span class="sxs-lookup"><span data-stu-id="56953-948">Adding a probe port</span></span>
- <span data-ttu-id="56953-949">Ao abrir a porta da sonda Olá Windows firewall</span><span class="sxs-lookup"><span data-stu-id="56953-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="56953-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Criar um nome de anfitrião virtual para a instância de SAP ASCS/SCS Olá em cluster</span><span class="sxs-lookup"><span data-stu-id="56953-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="56953-951">No Gestor de DNS do Windows hello, crie uma entrada DNS para o nome de anfitrião virtual Olá da instância ASCS/SCS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="56953-952">Olá endereço IP que atribuir o nome de anfitrião virtual toohello de Olá ASCS/SCS instância tem de ser Olá mesmo como endereço IP Olá que atribuiu tooAzure Balanceador de carga (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="56953-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="56953-953">Olá, endereço IP do nome de anfitrião de SAP ASCS/SCS virtual Olá (**pr1-ascs-sap**) é Olá mesmo como endereço IP de Olá do Balanceador de carga do Azure (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="56953-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definir a entrada DNS de Olá para o nome virtual do cluster de SAP ASCS/SCS Olá e o endereço de TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="56953-955">_**Figura 56:** definir Olá entrada DNS para o nome virtual do cluster de SAP ASCS/SCS Olá e o endereço de TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="56953-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="56953-956">toodefine Olá atribuído toohello anfitrião virtual nome de endereço IP, selecione **Gestor de DNS** > **domínio**.</span><span class="sxs-lookup"><span data-stu-id="56953-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Novo nome virtual e o endereço de TCP/IP para a configuração de cluster do SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="56953-958">_**Figura 57:** para configuração de cluster do SAP ASCS/SCS de endereços novo nome virtual e TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="56953-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="56953-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar Olá SAP primeiro nó de cluster</span><span class="sxs-lookup"><span data-stu-id="56953-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="56953-960">Executar Olá primeiro cluster nó opção no nó de cluster A. Por exemplo, num Olá **pr1-ascs-0** anfitrião.</span><span class="sxs-lookup"><span data-stu-id="56953-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="56953-961">portas de predefinição de Olá tookeep para Olá Azure interno Balanceador de carga, selecione:</span><span class="sxs-lookup"><span data-stu-id="56953-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="56953-962">**Sistema ABAP**: **ASCS** instância número **00**</span><span class="sxs-lookup"><span data-stu-id="56953-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="56953-963">**Sistema de Java**: **SCS** instância número **01**</span><span class="sxs-lookup"><span data-stu-id="56953-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="56953-964">**Sistema ABAP + Java**: **ASCS** instância número **00** e **SCS** instância número **01**</span><span class="sxs-lookup"><span data-stu-id="56953-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="56953-965">instância toouse números à 00 para Olá ABAP ASCS instância e 01 para a instância de Java SCS Olá, primeiro tem de toochange Olá do Azure de carga interno balanceador predefinido de balanceamento de carga regras, descritas em [carga do alteração Olá ASCS/SCS predefinido balanceamento de regras de Balanceador de carga interno do Azure Olá][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="56953-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="56953-966">Olá seguintes algumas tarefas não são descritas na documentação de instalação de SAP Olá padrão.</span><span class="sxs-lookup"><span data-stu-id="56953-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-967">Olá documentação de instalação do SAP descreve como tooinstall Olá primeiro nó de cluster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="56953-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="56953-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar o perfil SAP Olá da instância ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="56953-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="56953-969">É necessário tooadd um novo parâmetro de perfil.</span><span class="sxs-lookup"><span data-stu-id="56953-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="56953-970">parâmetro de perfil Olá impede que as ligações entre os processos de trabalho do SAP e o servidor de colocar em fila de Olá fechar quando estão inativos há demasiado tempo.</span><span class="sxs-lookup"><span data-stu-id="56953-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="56953-971">Iremos mencionado no cenário de problema de Olá [adicionar entradas de registo em ambos os nós de cluster de instância de SAP ASCS/SCS Olá][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="56953-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="56953-972">Na secção, introduzimos também dois parâmetros de ligação de TCP/IP básicos do alterações toosome.</span><span class="sxs-lookup"><span data-stu-id="56953-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="56953-973">No segundo passo, terá de tooset Olá colocar em fila servidor toosend um `keep_alive` assinalar para que as ligações de Olá não atingiu o limiar de inatividade do Balanceador de carga interno do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="56953-974">Olá toomodify perfil SAP da instância ASCS/SCS Olá:</span><span class="sxs-lookup"><span data-stu-id="56953-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="56953-975">Adicione este toohello de parâmetro de perfil perfil de instância do SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="56953-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="56953-976">No nosso exemplo, o caminho de Olá é:</span><span class="sxs-lookup"><span data-stu-id="56953-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="56953-977">Por exemplo, perfil de instância do SAP SCS toohello e caminho correspondente:</span><span class="sxs-lookup"><span data-stu-id="56953-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="56953-978">alterações de Olá tooapply, reiniciar a instância de SAP ASCS /SCS de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="56953-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Adicionar uma porta de pesquisa</span><span class="sxs-lookup"><span data-stu-id="56953-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="56953-980">Utilize o trabalho de configuração ao cluster completo do Olá de toomake do Balanceador de carga interno Olá sonda funcionalidade com o Balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="56953-981">Balanceador de carga interno do Azure Olá normalmente distribui a carga de trabalho de entrada Olá equitativamente entre participantes máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="56953-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="56953-982">No entanto, isto não funcionará em algumas configurações de cluster porque apenas uma instância está ativa.</span><span class="sxs-lookup"><span data-stu-id="56953-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="56953-983">Olá outra instância for passiva e não pode aceitar qualquer carga de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="56953-984">Uma funcionalidade de pesquisa ajuda-o quando atribui de Balanceador de carga interno do Azure Olá trabalham instância ativa tooan apenas.</span><span class="sxs-lookup"><span data-stu-id="56953-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="56953-985">Com a funcionalidade de pesquisa de Olá, o Balanceador de carga interno Olá pode detetar as instâncias ativas e apenas Olá instância com carga de trabalho Olá de destino, em seguida.</span><span class="sxs-lookup"><span data-stu-id="56953-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="56953-986">tooadd uma porta de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="56953-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="56953-987">Verifique Olá atual **ProbePort** definição executando o seguinte comando do PowerShell de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="56953-988">Executá-lo de dentro de uma das máquinas virtuais Olá numa configuração de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="56953-989">Defina uma porta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="56953-989">Define a probe port.</span></span> <span data-ttu-id="56953-990">número de porta de pesquisa do Olá predefinido é **0**.</span><span class="sxs-lookup"><span data-stu-id="56953-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="56953-991">No nosso exemplo, utilizamos a porta da sonda **62000**.</span><span class="sxs-lookup"><span data-stu-id="56953-991">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: porta Olá da sonda de configuração de cluster é 0 por predefinição][sap-ha-guide-figure-3048]

  <span data-ttu-id="56953-993">_**Figura 58:** porta de pesquisa de configuração de cluster predefinida Olá é 0_</span><span class="sxs-lookup"><span data-stu-id="56953-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="56953-994">número de porta de Olá está definido nos modelos de SAP Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="56953-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="56953-995">Pode atribuir o número de porta de Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56953-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="56953-996">tooset um novo valor ProbePort Olá  **SAP <*SID*> IP * * recurso de cluster, execute o seguinte script do PowerShell de Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="56953-997">Atualize as variáveis de PowerShell Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="56953-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="56953-998">Após a execução do script Olá, será pedido toorestart Olá SAP grupo tooactivate Olá as alterações de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

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

  <span data-ttu-id="56953-999">Depois de colocar Olá  **SAP <*SID*> * * online a função de cluster, certifique-se de que **ProbePort** está definido toohello novo valor.</span><span class="sxs-lookup"><span data-stu-id="56953-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Sonda a porta de cluster Olá depois de definir o novo valor de Olá][sap-ha-guide-figure-3049]

  <span data-ttu-id="56953-1001">_**Figura 59:** sonda a porta de cluster Olá depois de definir o novo valor de Olá_</span><span class="sxs-lookup"><span data-stu-id="56953-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="56953-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra a porta da sonda Olá Windows firewall</span><span class="sxs-lookup"><span data-stu-id="56953-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="56953-1003">É necessário tooopen uma porta de sonda de firewall do Windows em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="56953-1004">Utilize Olá seguinte script tooopen uma porta de sonda de firewall do Windows.</span><span class="sxs-lookup"><span data-stu-id="56953-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="56953-1005">Atualize as variáveis de PowerShell Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="56953-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="56953-1006">Olá **ProbePort** estiver definido demasiado**62000**.</span><span class="sxs-lookup"><span data-stu-id="56953-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="56953-1007">Agora pode aceder à partilha de ficheiros de Olá  **\\\ascsha-clsap\sapmnt** dos outros anfitriões, tais como de **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="56953-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="56953-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar a instância de base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="56953-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="56953-1009">base de dados do tooinstall Olá instância, siga o processo de Olá descrito em Olá documentação de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="56953-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar o segundo nó de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="56953-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="56953-1011">tooinstall Olá segundo cluster, siga os passos de Olá no Olá guia de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="56953-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Alterar tipo de início de Olá de instância de serviço do Windows do SAP ERS Olá</span><span class="sxs-lookup"><span data-stu-id="56953-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="56953-1013">Alterar o tipo de início de Olá de Olá serviço Windows do SAP ERS demasiado**automático (início atrasado)** em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="56953-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Altere o tipo de serviço Olá para Olá SAP ERS instância toodelayed automática][sap-ha-guide-figure-3050]

<span data-ttu-id="56953-1015">_**Figura 60:** alterar tipo de serviço Olá Olá SAP ERS instância toodelayed automática_</span><span class="sxs-lookup"><span data-stu-id="56953-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="56953-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Olá SAP primário o servidor de aplicações</span><span class="sxs-lookup"><span data-stu-id="56953-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="56953-1017">Instalar instância do servidor de aplicação principal (PAS) Olá <*SID*> - di - 0, na máquina virtual Olá que tiver designado toohost Olá PAS.</span><span class="sxs-lookup"><span data-stu-id="56953-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="56953-1018">Não existem nenhumas dependências nas definições específicas do DataKeeper ou do Azure.</span><span class="sxs-lookup"><span data-stu-id="56953-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="56953-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Olá SAP adicionais o servidor de aplicações</span><span class="sxs-lookup"><span data-stu-id="56953-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="56953-1020">Instale um servidor SAP aplicação adicionais (AAS) em todas as máquinas de virtuais Olá que lhe tiver designado toohost uma instância de servidor de aplicações SAP.</span><span class="sxs-lookup"><span data-stu-id="56953-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="56953-1021">Por exemplo, num <*SID*> - di - 1 demasiado <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="56953-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="56953-1022">Isto conclusão da instalação de Olá de um sistema de SAP NetWeaver de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="56953-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="56953-1023">Em seguida, prossiga com a ativação pós-falha de teste.</span><span class="sxs-lookup"><span data-stu-id="56953-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="56953-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testar a ativação pós-falha de instância do SAP ASCS/SCS Olá e replicação SIOS</span><span class="sxs-lookup"><span data-stu-id="56953-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="56953-1025">É fácil tootest e monitorizar uma ativação pós-falha de instância do SAP ASCS/SCS e a replicação de discos SIOS utilizando o Gestor de clusters de ativação pós-falha e a ferramenta de configuração e gestão de DataKeeper SIOS Olá.</span><span class="sxs-lookup"><span data-stu-id="56953-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="56953-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>Instância do SAP ASCS/SCS está em execução no nó de cluster A</span><span class="sxs-lookup"><span data-stu-id="56953-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="56953-1027">Olá **SAP PR1** grupo de cluster está em execução no nó de cluster A. Por exemplo, num **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="56953-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="56953-1028">Atribuir a unidade de disco de Olá partilhado S, que faz parte do Olá **SAP PR1** grupo e utiliza a que instância ASCS/SCS Olá, toocluster recomeço de nó do cluster</span><span class="sxs-lookup"><span data-stu-id="56953-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Figura 61: Gestor de clusters de ativação pós-falha: grupo de cluster do SAP < SID > olá está em execução no nó de cluster A][sap-ha-guide-figure-5000]

<span data-ttu-id="56953-1030">_**Figura 61:** Gestor de clusters de ativação pós-falha: Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster A_</span><span class="sxs-lookup"><span data-stu-id="56953-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="56953-1031">Olá SIOS DataKeeper gestão e a ferramenta de configuração, pode ver esse disco partilhado de Olá os dados são replicados em sincronia de Olá origem volume unidade S no nó de cluster de uma unidade de volume de destino S de toohello num nó de cluster B. Por exemplo, são replicado desde **pr1-ascs-0 [10.0.0.40]** demasiado**pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="56953-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: No SIOS DataKeeper, replicar volume local Olá do nó de cluster de um nó de toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="56953-1033">_**Figura 62:** no SIOS DataKeeper, replicar volume local Olá a partir do nó de cluster de um nó de toocluster B_</span><span class="sxs-lookup"><span data-stu-id="56953-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="56953-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>A ativação pós-falha do nó A toonode B</span><span class="sxs-lookup"><span data-stu-id="56953-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="56953-1035">Escolha uma das tooinitiate opções uma ativação pós-falha da Olá SAP <*SID*> grupo de cluster de nó A toocluster do nó do cluster b:</span><span class="sxs-lookup"><span data-stu-id="56953-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="56953-1036">Utilize o Gestor de clusters de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="56953-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="56953-1037">Utilizar o PowerShell do Cluster de ativação pós-falha</span><span class="sxs-lookup"><span data-stu-id="56953-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="56953-1038">Reiniciar um nó de cluster no sistema de operativo convidado de Windows hello (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="56953-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="56953-1039">Reinicie o nó de cluster A partir do portal do Azure de Olá (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="56953-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="56953-1040">Reiniciar um nó de cluster utilizando o Azure PowerShell (esta ação inicia uma ativação pós-falha automática de Olá SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="56953-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="56953-1041">Após a ativação pós-falha, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B. Por exemplo, que é executada **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="56953-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: No Gestor de clusters de ativação pós-falha, grupo de cluster do SAP < SID > olá está em execução no nó de cluster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="56953-1043">_**Figura 63**: na ativação pós-falha Gestor de clusters, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B_</span><span class="sxs-lookup"><span data-stu-id="56953-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="56953-1044">Olá disco partilhado está agora montado no cluster de nó B. SIOS DataKeeper está a replicar dados do disco de volume de origem S no cluster nó B tootarget volume unidade S no nó de cluster A. Por exemplo, está a replicar de **pr1-ascs-1 [10.0.0.41]** demasiado**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="56953-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica volume local Olá nó B toocluster do nó do cluster A][sap-ha-guide-figure-5003]

  <span data-ttu-id="56953-1046">_**Figura 64:** SIOS DataKeeper replica volume local Olá nó B toocluster do nó do cluster A_</span><span class="sxs-lookup"><span data-stu-id="56953-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
