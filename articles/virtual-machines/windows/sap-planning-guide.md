---
title: "aaaSAP NetWeaver em VMs do Azure – planeamento e implementação | Microsoft Docs"
description: "SAP NetWeaver em máquinas virtuais do Azure (VMs) – planeamento e o guia de implementação"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 2b58a419-c892-4722-8cb6-2f8beef4430c
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53d63240760282b409f7e9412e8240689bcbcc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--planning-and-implementation-guide"></a>SAP NetWeaver no Azure Windows as máquinas virtuais (VMs) – planeamento e o guia de implementação
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/sap-get-started.mdsap-dbms-guide.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.mdsap-dbms-guide.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.mdsap-dbms-guide.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.mdsap-dbms-guide.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.mdsap-dbms-guide.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.mdsap-dbms-guide.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#step-2-create-vm-image
[virtual-machines-windows-capture-image]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Microsoft Azure permite que as empresas tooacquire computação e recursos de armazenamento no tempo mínimo sem ciclos de aprovisionamento demorado. Máquinas virtuais do Azure permite que as empresas toodeploy classical aplicações, como o SAP NetWeaver com base em aplicações no Azure e expandir os respetivos fiabilidade e disponibilidade sem ter ainda mais recursos disponíveis no local. Serviços de Máquina Virtual do Azure também suporta a conectividade entre instalações, tooactively de empresas que permite integrar Virtual Machines do Azure para os seus domínios no local, as respetivas nuvens privadas e as respetivas horizontal de sistema do SAP.
Este documento técnico descreve as noções básicas de Olá do Microsoft Azure Virtual Machine e fornece instruções de considerações de planeamento e implementação para as instalações do SAP NetWeaver no Azure e como tal, deve ser Olá documento tooread antes de iniciar implementações reais do SAP NetWeaver no Azure.
Olá documento complementa Olá SAP instalação documentação e notas de SAP que representam os recursos de primário Olá para as instalações e implementações de software de SAP indicado plataformas.

## <a name="summary"></a>Resumo
É um termo bastante utilizado que é obtenham mais importância dentro Olá da indústria IT, de pequenas empresas segurança toolarge e multinational as empresas têm a informática em nuvem.

Microsoft Azure é Olá plataforma de serviços em nuvem da Microsoft que oferece um largo espetro de possibilidades de novo. Agora os clientes são toorapidly capaz de aprovisionar e aprovisionar desativação aplicações como um serviço numa nuvem Olá, pelo que não são limitado tootechnical ou budgeting restrições. Em vez de investir tempo e orçamento na infraestrutura de hardware, as empresas podem concentrar-se na aplicação Olá, os processos de negócios e suas vantagens para os clientes e utilizadores.

Com os Serviços da Máquina Virtual do Microsoft Azure, a Microsoft oferece uma plataforma completa de Infraestrutura como um Serviço (IaaS). As aplicações baseadas em SAP NetWeaver são suportadas em Máquinas Virtuais do Azure (IaaS). Este documento descreve como tooplan e implementar SAP NetWeaver com base em aplicações no Microsoft Azure como plataforma Olá à escolha.

documento de Olá próprio irá focar-se em dois aspetos principais:

* primeira parte do Olá descreve dois padrões de implementação suportado para aplicações de NetWeaver SAP com base no Azure. Também descrevem processamento geral do Azure com as implementações de SAP em mente.
* segunda parte do Olá pormenor implementar Olá dois diferentes cenários descritos na primeira parte do Olá.

Para obter recursos adicionais, consulte capítulo [recursos] [ planning-guide-1.2] neste documento.

### <a name="definitions-upfront"></a>Definições de compromisso
Ao longo do documento Olá utilizaremos Olá seguintes termos:

* IaaS: Infraestrutura como um serviço.
* PaaS: Plataforma como serviço.
* SaaS: Software como um serviço.
* ARM: O Azure Resource Manager
* Componente SAP: uma individuais SAP aplicação tal como ECC, BW, Gestor de solução ou EP.  Componentes SAP podem ser baseados em tecnologias tradicionais ABAP ou Java ou uma aplicação não baseada em NetWeaver como objetos de negócio.
* Ambiente de SAP: um ou mais componentes do SAP agrupadas logicamente tooperform uma função de negócio, tais como o desenvolvimento, QAS, formação, DR ou de produção.
* SAP horizontal: Isto refere-se toohello todos SAP recursos um cliente horizontal IT. Olá horizontal SAP inclui todos os ambientes de não produção e produção.
* Sistema SAP: combinação de Olá de camada DBMS e a camada de aplicação de por exemplo, um sistema de desenvolvimento do SAP ERP, sistema de teste de SAP BW, sistema de produção do SAP CRM, etc.. No Azure implementações não é suportada a toodivide estas duas camadas entre no local e o Azure. Isto significa que um sistema SAP é implementado no local ou está implementado no Azure. No entanto, pode implementar Olá sistemas diferentes de um horizontal SAP para o Azure ou no local. Por exemplo, pode implementar Olá SAP CRM desenvolvimento e teste sistemas no Azure mas Olá SAP CRM produção sistema no local.
* Implementação apenas de nuvem: uma implementação onde Olá subscrição do Azure não está ligado através de um site para site ou a infraestrutura de rede do ExpressRoute ligação toohello no local. Em comum documentação do Azure estes tipos de implementações também estão descritos como implementações 'Na nuvem-Only'. Máquinas virtuais implementadas com este método são acedidas através de Olá internet e um endereço IP público e/ou um DNS público nome atribuído toohello VMs no Azure. Para o Microsoft Windows hello no local do Active Directory (AD) e DNS não estiver expandido tooAzure nestes tipos de implementações. Por conseguinte, VMs Olá não fazem parte do Olá no local do Active Directory. Mesmo se aplica para implementações de Linux utilizando, por exemplo, OpenLDAP + Kerberos.

> [!NOTE]
> As implementações de apenas na nuvem neste documento é definida como concluídas SAP landscapes estão em execução no modo exclusivo no Azure sem a extensão do Active Directory / OpenLDAP ou resolução de nomes no local na nuvem pública. Configurações de apenas na nuvem não são suportadas para sistemas de SAP de produção ou configurações de onde SAP STMS ou outros recursos no local têm toobe utilizado entre sistemas SAP alojados no Azure e recursos que residem no local.
>
>

* Em vários locais: Descreve um cenário onde as VMs são implementado tooan subscrição do Azure com o site a site, vários site ou de conectividade do ExpressRoute entre datacenter(s) do Olá no local e o Azure. Documentação do Azure em comum, estes tipos de implementações também estão descritos como cenários de vários locais. motivo Olá para ligação Olá é tooextend domínios no local, no local do Active Directory / OpenLDAP e no local DNS no Azure. Olá no local horizontal é expandida toohello recursos do Azure da subscrição Olá. Com esta extensão, Olá VMs pode fazer parte do domínio do Olá no local. Utilizadores de domínio do domínio do Olá no local podem aceder a servidores de Olá e podem executar serviços nessas VMs (por exemplo, o DBMS serviços). É possível resolução do nome e a comunicação entre as VMs implementadas no local e as VMs implementadas do Azure. Este é o cenário de Olá que Esperamos que a maioria dos toobe de ativos SAP implementada no.  Consulte [isto] [ vpn-gateway-cross-premises-options] artigo e [isto] [ vpn-gateway-site-to-site-create] para obter mais informações.

> [!NOTE]
> Implementações de vários locais dos sistemas SAP onde com sistemas SAP de Virtual Machines do Azure são membros de um domínio no local são suportadas para sistemas de SAP de produção. Configurações em vários locais são suportadas para a implementação de partes ou concluir SAP landscapes no Azure. Mesmo em execução horizontal SAP concluída Olá no Azure necessita de ter as VMs que está a ser parte do domínio no local e anúncios / OpenLDAP. Em versões anteriores do documentação Olá falamos sobre cenários híbridos-IT, onde o termo Olá 'Híbrida' tem Root no facto de Olá se há uma conetividade em vários locais entre no local e o Azure. Plus, facto Olá esse Olá VMs no Azure fazem parte do Olá no local do Active Directory / OpenLDAP.
>
>

Alguma documentação do Microsoft descreve cenários de vários locais um pouco diferente, especialmente para configurações DBMS HA. Além Olá maiúsculas e minúsculas de Olá SAP relacionadas documentos, cenário Olá em vários locais apenas boils baixo toohaving um site para site ou privado (ExpressRoute) conectividade e Olá facto que horizontal SAP Olá é distribuído entre no local e o Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Recursos
Olá seguintes guias adicionais estão disponíveis para o tópico de Olá das implementações de SAP no Azure:

* [SAP NetWeaver em Azure Virtual Machines (VMs) – (deste documento) do guia de implementação e planeamento][planning-guide]
* [SAP NetWeaver em máquinas virtuais do Azure (VMs) – guia de implementação][deployment-guide]
* [SAP NetWeaver em máquinas virtuais do Azure (VMs) – DBMS guia de implementação][dbms-guide]
* [SAP NetWeaver em máquinas virtuais do Azure (VMs) – guia de implementação de elevada disponibilidade][ha-guide]

> [!IMPORTANT]
> Onde quer que é utilizado possíveis toohello uma ligação que faça referência guia de instalação do SAP (referência InstGuide-01, consulte <http://service.sap.com/instguides>). Quando se trata toohello pré-requisitos e o processo de instalação, guias de instalação do Olá SAP NetWeaver deve ser sempre Leia com atenção, como deste documento abrange apenas a tarefas específicas para sistemas de SAP NetWeaver instalado no Microsoft Azure Máquina Virtual.
>
>

Olá segue SAP notas é tópico toohello relacionados do SAP no Azure:

| Número de nota | Título |
| --- | --- |
| [1928533] |Aplicações SAP no Azure: os produtos e dimensionamento suportados |
| [2015553] |SAP no Microsoft Azure: suporta a pré-requisitos |
| [1999351] |Resolução de problemas avançada monitorização do Azure para SAP |
| [2178632] |Chave de monitorização métricas para SAP no Microsoft Azure |
| [1409604] |Virtualização no Windows: avançada de monitorização |
| [2191498] |SAP no Linux com o Azure: avançada de monitorização |
| [2243692] |Linux no Microsoft Azure (IaaS) VM: problemas de licença do SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: Notas de instalação |
| [2002167] |Red Hat Enterprise Linux 7. x: instalação e a atualização |

Leia também Olá [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) que contém todas as notas de SAP para o Linux.

Limitações gerais predefinido e limitações máximas de subscrições do Azure podem ser encontradas na [neste artigo][azure-subscription-service-limits-subscription]

## <a name="possible-scenarios"></a>Cenários possíveis
SAP, muitas vezes, é apresentado como uma das aplicações mais fundamentais do Olá em empresas. arquitetura de Olá e as operações destas aplicações principalmente é muito complexa e assegurar que cumpre os requisitos de desempenho e disponibilidade é importante.

Deste modo, as empresas têm toothink cuidadosamente sobre os quais as aplicações podem ser executadas num ambiente de nuvem pública, independentemente do fornecedor de nuvem Olá escolhido.

Tipos de sistema possíveis para a implementação SAP NetWeaver com base em aplicações na nuvem pública ambientes estão listados abaixo:

1. Sistemas de produção de tamanho médio
2. Sistemas de desenvolvimento
3. Sistemas de teste
4. Sistemas de protótipo
5. Learning / sistemas de demonstração

Na ordem toosuccessfully implementar sistemas SAP para o IaaS do Azure ou para o IaaS em geral, é importante toounderstand Olá significativas as diferenças entre as ofertas de Olá outsourcers tradicionais ou de que os fornecedores e ofertas de IaaS. Enquanto o fornecedor de alojamento tradicional Olá ou outsourcer irá adaptar a carga de trabalho do infraestrutura (tipo de rede, armazenamento e servidor) toohello um cliente pretende toohost, em vez disso, é responsabilidade toochoose Olá direita carga de trabalho do cliente Olá para implementações IaaS.

Como primeiro passo, o que os clientes precisam Olá tooverify seguintes itens:

* Olá SAP suportados tipos VM do Azure
* Olá SAP suportado produtos/versões no Azure
* Olá suportadas versões do SO e DBMS para Olá que SAP específico versões no Azure
* Débito SAPS fornecido pelo SKUs diferentes do Azure

Olá respostas toothese perguntas podem ser lidos na nota SAP [1928533].

Limitações de largura de banda e de recursos do Azure como um segundo passo, tem de toobe em comparação com consumo de recursos de tooactual dos sistemas no local. Por conseguinte, os clientes necessidade toobe familiarizar com Olá funcionalidades diferentes do Olá Azure tipos suportados com SAP na área de Olá de:

* Recursos de CPU e memória de diferentes tipos VM e
* Largura de banda IOPS de diferentes tipos VM e
* Capacidades de rede de diferentes tipos VM.

A maioria dos dados pode ser encontrada [aqui][virtual-machines-sizes]

Tenha em atenção que Olá limites indicados na ligação de Olá acima são os limites superiores. Não significa que limita a Olá para qualquer um dos recursos de Olá, por exemplo, o IOPS podem ser fornecido em todas as circunstâncias. exceções de Olá são recursos de CPU e memória Olá de um tipo VM que escolheu. Para tipos VM de Olá suportados pelo SAP, recursos de CPU e memória Olá estão reservados e como tal, disponível em qualquer ponto no tempo para consumo dentro Olá VM.

plataforma do Microsoft Azure Olá como outras plataformas de IaaS é uma plataforma de multi-inquilino. Isto significa que o armazenamento, rede e outros recursos são partilhados entre inquilinos. Lógica de limitação e quota inteligente é utilizada tooprevent um inquilino do afetar o desempenho de Olá de outro inquilino (vizinho inúteis) de uma forma drastic. Embora a lógica na Azure tradas variações como de tookeep em plataformas de pequena e partilhado de elevada disponibilidade de largura de banda teve tendem variações como maior de toointroduce na disponibilidade de recursos/largura de banda que muitos clientes é utilizado tooin as respetivas implementações no local. Como resultado, podem ocorrer diferentes níveis de largura de banda no que diz respeito toonetworking ou o armazenamento e/s (volume Olá, bem como latência) de toominute minuto. probabilidade Olá que um sistema SAP no Azure foi experiência variações como maior do que um sistema local tem toobe levado em consideração.

Um último passo consiste tooevaluate requisitos de disponibilidade. Pode acontecer, esse Olá subjacente a infraestrutura do Azure tem tooget atualizado e necessita de anfitriões de Olá com toobe VMs reiniciado. Nestes casos, as VMs em execução nesses anfitriões seriam possível desligadas e reiniciadas bem. Temporização Olá essas manutenção é efetuada durante o horário comercial de não-core de uma determinada região mas janela potenciais Olá de algumas horas durante o qual um computador será reiniciado é relativamente grande. Existem várias tecnologias dentro Olá plataforma Azure que pode ser configurado toomitigate alguns ou todos os Olá afetam a essas atualizações. Melhoramentos futuros de Olá plataforma do Azure, aplicação DBMS e SAP são concebidos toominimize impacto Olá essas reinícios.

Toosuccessfully de implementar um sistema SAP para o Azure, hello no local SAP sistemas sistema operativo, a base de dados e aplicações SAP deve aparecer no Olá matriz de suporte do Azure de SAP, cabem dentro Olá de recursos de Olá pode fornecer a infraestrutura do Azure e que pode trabalhar com Olá que disponibilidade SLAs Microsoft Azure oferece. Como esses sistemas são identificados, terá de toodecide dos Olá seguir dois cenários de implementação.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Apenas na nuvem - implementações de Máquina Virtual no Azure sem dependências no Olá no local a rede de cliente
![VM único com o cenário de formação implementado no Azure ou de demonstração SAP][planning-guide-figure-100]

Este cenário é comum para trainings ou sistemas de demonstração, onde todos os componentes de Olá de SAP e o software de SAP não estão instalados dentro de uma única VM. Sistemas de SAP de produção não são suportados neste cenário de implementação. Em geral, este cenário cumpre os requisitos de Olá:

* Olá VMs estão acessíveis através da rede pública Olá. Conectividade de rede diretamente para aplicações de Olá em execução dentro Olá VMs toohello no local rede da empresa ou Olá proprietário Olá demonstrações trainings conteúdo ou cliente Olá não é necessário.
* Em caso de várias VMs que representam o cenário de demonstração ou trainings Olá, resolução do nome e de comunicações de rede necessita de toowork entre Olá VMs. Mas toobe isolado, para que vários conjuntos de VMs podem ser implementados lado sem interferências necessita de comunicações entre o conjunto de Olá de VMs.  
* A conectividade à Internet é necessária para o início de sessão do Olá utilizador final tooremote para toohello que VMS alojadas no Azure. Dependendo de SO convidado Olá, é utilizado o serviços de Terminal/RDS ou VNC/ssh tooaccess Olá VM tooeither realizar tarefas de preparação de Olá ou efetuar demonstrações Olá. Se o SAP portas, tais como 3200, 3300 & 3600 podem também ser expostos instância da aplicação Olá SAP pode ser acedida a partir de qualquer ambiente de trabalho ligada à Internet.
* Olá SAP sistemas (e VM(s)) representam um cenário de autónomo no Azure que apenas requer acesso à internet pública de acesso de utilizador final e não necessita de uma ligação tooother VMs no Azure.
* SAPGUI e um browser instalados e executadas diretamente no Olá VM.
* Não são necessárias uma reposição de um estado original do VM toohello rápida e novo novamente a implementação desse estado original.
* No caso de Olá de demonstração e cenários de formação que são realizados em várias VMs, um Active Directory / serviço OpenLDAP e/ou de DNS é necessário para cada conjunto de VMs.

![Grupo de VMS que representa uma demonstração ou cenário de formação num serviço em nuvem do Azure][planning-guide-figure-200]

É importante tookeep em atenção que Olá VM em cada um dos Olá define toobe necessidade implementado em paralelo, onde os nomes VM Olá em cada conjunto de Olá são Olá-mesmo.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>em vários locais - implementação única ou várias VMs SAP no Azure com o requisito de Olá de que está a ser totalmente integrados em rede no local de Olá
![VPN com conectividade de Site para Site (em vários locais)][planning-guide-figure-300]

Este cenário é um cenário de vários locais com muitos padrões de implementação possível. Pode ser descrito simplesmente como como executar algumas partes do Olá SAP horizontal no local e outras partes do Olá horizontal SAP no Azure. Todos os aspetos do facto de Olá parte dos componentes SAP Olá estão em execução no Azure devem estar transparentes para os utilizadores finais. Olá, por conseguinte, a comunicação de RFC, SAP transporte correção de sistema (STMS), a segurança (por exemplo, SSO) e impressão, etc. irá funcionar de forma totalmente integrada para os sistemas SAP Olá em execução no Azure. Mas cenário entre locais de Olá também descreve um cenário onde horizontal SAP concluída Olá é executada no Azure com o domínio do cliente Olá e DNS expandido no Azure.

> [!NOTE]
> Este é o cenário de implementação de Olá que é suportado para a execução de sistemas SAP produtivos.
>
>

Leitura [neste artigo] [ vpn-gateway-create-site-to-site-rm-powershell] para obter mais informações sobre como tooconnect tooMicrosoft Azure de rede no local

> [!IMPORTANT]
> Quando é se fala sobre cenários de vários locais entre implementações de cliente do Azure e no local, podemos procura granularidade Olá dos sistemas SAP todo. Cenários que são *não suportado* para vários locais cenários são:
>
> * Executar diferentes camadas de aplicações SAP em métodos de implementação diferentes. Por exemplo, executar Olá DBMS camada no local, mas camada da aplicação Olá SAP em VMs implementadas como VMs do Azure ou vice-versa.
> * Alguns componentes de uma camada SAP no Azure e alguns no local. Por exemplo, dividir as instâncias da camada de aplicação Olá SAP no local e as VMs do Azure.
> * Não é suportada a distribuição de VMs instâncias em execução SAP de um sistema através de várias regiões do Azure.
>
> motivo Olá estas restrições é o requisito de Olá para uma rede de elevado desempenho muito baixa latência dentro de um sistema SAP, especialmente entre instâncias da aplicação Olá e Olá DBMS uma camada de um sistema SAP.
>
>

### <a name="supported-os-and-database-releases"></a>SO e versões de base de dados suportados
* Software de servidor de Microsoft suportado para serviços de Máquina Virtual do Azure está listado neste artigo: <http://support.microsoft.com/kb/2721672>.
* Versões do sistema da base de dados suportadas nos serviços de Máquina Virtual do Azure em conjunto com o software SAP suportadas versões do sistema de operativo, estão documentadas na nota SAP [1928533].
* Aplicações SAP e versões suportadas nos serviços de Máquina Virtual do Azure estão documentadas na nota SAP [1928533].
* Apenas imagens de 64 bits estão toorun suportado como convidado VMs no Azure para cenários SAP. Isto também significa que apenas aplicações de SAP de 64 bits e as bases de dados são suportados.

## <a name="microsoft-azure-virtual-machine-services"></a>Serviços de Máquina Virtual do Microsoft Azure
plataforma do Microsoft Azure de Olá é uma nuvem de escala de internet plataforma de serviços alojados e que operava nos dados do Microsoft centros. plataforma de Olá inclui serviços de Máquina Virtual (infraestrutura como um serviço ou IaaS) do Olá Microsoft Azure e um conjunto de plataforma avançado, como um capacidades de serviço (PaaS).

Olá plataforma Azure reduz a necessidade de Olá da tecnologia prévio e comprar de infraestrutura. Simplifica a manutenção e a funcionar aplicações fornecendo toohost de armazenamento e computação a pedido, dimensionar e gerir a aplicação web e aplicações ligadas. Gestão de infraestrutura é automatizada com uma plataforma que foi concebida para elevada disponibilidade e dimensionamento toomatch necessidades de utilização com a opção de Olá de um modelo de preços pay as you go dinâmico.

![Posicionamento dos serviços de Máquina Virtual do Microsoft Azure][planning-guide-figure-400]

Com os serviços de Máquina Virtual do Azure, Microsoft é permitindo tooAzure de imagens de servidor personalizado toodeploy como instâncias de IaaS (consulte a figura 4). Olá máquinas virtuais no Azure se baseiam em unidades de disco rígido virtuais (VHD) de Hyper-V e são toorun capaz de sistemas operativos diferentes, como o SO convidado.

Perspetiva de um operacional, Olá que Service de Máquina Virtual do Azure oferece semelhante experiências como máquinas virtuais implementadas no local. No entanto, tem vantagem significativa Olá e que não precisa de tooprocure, administrar e gerir a infraestrutura de Olá. Os programadores e os administradores têm controlo total da imagem do sistema operativo Olá das máquinas virtuais. Os administradores podem iniciar sessão remotamente para manutenção de tooperform essas máquinas virtuais e a resolução de problemas de tarefas, bem como as tarefas de implementação de software. No regard toodeployment, restrições apenas Olá são os tamanhos de Olá e capacidades das VMs do Azure. Estes podem não ser bem como granulares numa configuração de como isto foi feito no local. Há uma opção de tipos VM que representam uma combinação de:

* Número de vCPUs,
* Memória,
* Número de VHDs que podem ser anexados
* Larguras de banda de rede e armazenamento.

tamanho de Olá e limitações de vários tamanhos de diferentes máquinas virtuais oferecidas podem ser vistos numa tabela no [neste artigo][virtual-machines-sizes]

Como irá tenha em consideração existem diferentes famílias ou série de máquinas virtuais. A partir de Dec de 2015, pode distinguir Olá famílias de VMs a seguir:

* Tipos de a0 A7 VM: não todas essas são certificadas para SAP. Primeiro série VM que foi introduzida IaaS do Azure com.
* Tipos de a8-A11 VM: as instâncias de computação de alto desempenho. Em execução em efetuar uma melhor diferentes anfitriões que outras VMs de uma série de computação.
* Tipos de VM de série D: melhor efetuar a A0 A7. Nem todos os tipos VM Olá são certificados com SAP.
* Tipos de VM-série DS: utilizar o mesmos anfitriões como série D, mas são tooAzure tooconnect capaz de armazenamento Premium (consulte o capítulo [Premium Storage do Azure] [ planning-guide-3.3.2] deste documento). Novo nem todos os tipos VM são certificados com SAP.
* Tipos de VM de série de G: tipos VM de elevada da memória.
* Tipos de VM de série GS: como G série mas incluindo Olá opção toouse Premium Storage do Azure (consulte o capítulo [Premium Storage do Azure] [ planning-guide-3.3.2] deste documento). Ao utilizar VMs de série GS como servidores de base de dados é obrigatória toouse Premium Storage para ficheiros de registo de dados e a transação de base de dados

Pode encontrar Olá mesmas configurações de CPU e memória na série VM diferente. Contudo, ao procurar o desempenho de débito Olá destas VMs fora de série de diferentes Olá poderá diferem significativamente. Apesar de ter Olá mesma configuração de CPU e memória. Razão é que Olá anfitrião server hardware subjacente no introdução Olá de diferentes tipos de VM Olá tinha características de débito diferentes.  Normalmente, diferença Olá mostrada no desempenho de débito também é refletida no preço Olá Olá diferentes VMs.

Tenha em atenção que não todas as diferente série VM poderá ser-lhe oferecida em cada uma das Olá regiões do Azure (para regiões do Azure Consulte seguinte capítulo). Lembre-se também de que nem todas as VMs ou série de VM é certificada para SAP.

> [!IMPORTANT]
> Utilização de Olá de NetWeaver SAP com base em aplicações, apenas Olá subconjunto de configurações e os tipos VM listadas na nota SAP [1928533] são suportados.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Regiões do Azure
Microsoft permite toodeploy máquinas virtuais para, por isso, chamado 'regiões do Azure". Uma região do Azure pode ser um ou vários centros de dados que se encontrem próximos. Para a maioria Olá regiões geopolíticas no mundo Olá Microsoft tem, pelo menos, duas regiões do Azure. Por exemplo, na Europa há uma região do Azure de 'Europa do Norte' e um dos 'Europa Ocidental'. Estas duas regiões do Azure numa região geopolítica são separadas por distância significativa suficiente para que perante desastres naturais ou técnicas não afetam ambas as regiões do Azure no Olá mesma região geopolítica. Uma vez que a Microsoft está aumentar firmemente a criar os novos regiões do Azure em diferentes regiões geopolíticas global, o número de Olá destas regiões aumentar firmemente está a crescer e a partir de 2015 Dec atingido o número de Olá de 20 regiões do Azure com regiões adicionais anunciadas já. Como um cliente pode implementar sistemas SAP para todas as estas regiões, incluindo regiões do Azure de Olá dois na China. Para atual segurança toodate informações sobre regiões do Azure, consulte o este Web site: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Olá conceito de Máquina Virtual do Microsoft Azure
Microsoft Azure oferece uma infraestrutura como um toohost da solução de serviço (IaaS) máquinas virtuais com funcionalidades semelhantes como uma solução de virtualização no local. É capaz de máquinas virtuais a partir de toocreate dentro Olá Portal do Azure, PowerShell ou o CLI, que também oferecem capacidades de gestão e implementação.

O Azure Resource Manager permite-lhe tooprovision das suas aplicações com um modelo declarativo. Num único modelo, pode implementar vários serviços, bem como as respetivas dependências. Utilizar Olá mesmo modelo toorepeatedly implementar a aplicação durante cada fase do ciclo de vida da aplicação Olá.

Obter mais informações sobre como utilizar os modelos ARM podem ser encontradas aqui:

* [Implementar e gerir máquinas virtuais utilizando modelos Azure Resource Manager e Olá CLI do Azure][virtual-machines-linux-cli-deploy-templates]
* [Gerir máquinas virtuais utilizando o Azure Resource Manager e o PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://Azure.microsoft.com/Documentation/Templates/>

Outra funcionalidade interessante é imagens toocreate de capacidade de Olá provenientes de máquinas virtuais, que lhe permite tooprepare determinada repositórios a partir do qual é capaz de tooquickly implementar instâncias de Máquina Virtual que satisfaçam os requisitos.

Podem encontrar mais informações sobre como criar imagens de máquinas virtuais no [neste artigo (Windows)] [ virtual-machines-windows-capture-image] ou no [neste artigo (Linux)][virtual-machines-linux-capture-image].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domínios de falhas
Domínios de falhas representam uma unidade física de falha, infraestrutura física toohello muito estritamente relacionados nos centros de dados e um painel físico ou um bastidor pode ser considerado um domínio de falhas, não existe nenhum mapeamento um para um direto entre Olá dois.

Quando implementar várias máquinas virtuais como parte de um sistema SAP nos serviços de Máquina Virtual do Microsoft Azure, pode a influenciar Olá toodeploy de controlador de recursos do Azure da aplicação em diferentes domínios de falhas, aumentando assim que cumprem os requisitos de Olá de Olá SLA do Microsoft Azure. No entanto, Olá distribuição de domínios de falhas através de uma unidade de escala do Azure (coleção de centenas de nós de computação ou nós de armazenamento e redes) ou atribuição Olá de VMs tooa domínio de falhas específico é algo durante o qual não tem direcionar o controlo. Ordem toodirect Olá recursos de infraestrutura do Azure controlador toodeploy um conjunto de VMs através de domínios de falhas diferente, terá de tooassign um toohello do conjunto de disponibilidade do Azure VMs no momento da implementação. Para obter mais informações sobre conjuntos de disponibilidade do Azure, consulte o capítulo [conjuntos de disponibilidade do Azure] [ planning-guide-3.2.3] neste documento.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Domínios de atualização
Domínios de atualização representam uma unidade lógica que ajudam a toodetermine como uma VM dentro de um sistema SAP, que consiste em instâncias SAP em execução em várias VMs, será atualizada. Quando ocorre uma atualização, o Microsoft Azure passa pelo processo de Olá de atualizar estes domínios de atualização de um de cada. Por propagando-se as VMs no momento da implementação através de domínios de atualização diferentes pode proteger o sistema SAP parcialmente de potenciais períodos de inatividade. Na ordem tooforce Azure toodeploy Olá VMs de um sistema SAP distribuídas por domínios de atualização diferentes, tem de tooset um atributo específico no momento da implementação de cada VM. Domínios de tooFault semelhante, uma unidade de escala do Azure está dividido em vários domínios de atualização. Ordem toodirect Olá recursos de infraestrutura do Azure controlador toodeploy um conjunto de VMs através de domínios de atualização diferentes, terá de tooassign um toohello do conjunto de disponibilidade do Azure VMs no momento da implementação. Para obter mais informações sobre conjuntos de disponibilidade do Azure, consulte o capítulo [conjuntos de disponibilidade do Azure] [ planning-guide-3.2.3] abaixo.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Conjuntos de disponibilidade do Azure
Máquinas virtuais do Azure dentro de um conjunto de disponibilidade de Azure serão distribuídas por Olá controlador de recursos do Azure através de diferentes falhas e de domínios de atualização. objetivo Olá distribuição Olá através de diferentes falhas e de domínios de atualização é tooprevent que todas as VMs de um sistema SAP da que está a ser encerradas no caso de Olá de manutenção da infraestrutura ou de uma falha de dentro de um domínio de falhas. Por predefinição, as VMs não fazem parte de um conjunto de disponibilidade. participação de Olá de uma VM num conjunto de disponibilidade está definida no momento da implementação ou mais tarde por uma reconfiguração e a implementação de uma VM.

conceito de Olá toounderstand de forma de conjuntos de disponibilidade do Azure e Olá conjuntos de disponibilidade se relacionam com tooFault e domínios de atualização, leia [neste artigo][virtual-machines-manage-availability]

conjuntos de disponibilidade de toodefine para ARM através de um modelo json consulte [Olá especificações de api de rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) e procure "availability".

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Armazenamento: Armazenamento do Microsoft Azure e os discos de dados
Máquinas virtuais do Microsoft Azure utilizar tipos de armazenamento diferente. Quando implementar SAP nos serviços de Máquina Virtual do Azure, é importante toounderstand Olá diferenças estes dois principais tipos de armazenamento:

* Armazenamento voláteis não persistente.
* Armazenamento persistente.

o armazenamento não persistentes Olá é ligado diretamente ao toohello máquinas virtuais em execução e reside em nós de computação de Olá próprios – armazenamento de instância local do Olá (armazenamento temporário). tamanho de Olá depende do tamanho de Olá de Olá Máquina Virtual escolhido quando Olá implementação iniciada. Este tipo de armazenamento é volátil e, por conseguinte, o disco de Olá é inicializado quando uma instância de Máquina Virtual for reiniciada. Normalmente, o ficheiro de paginação Olá para sistema de operativo Olá está localizado neste disco temporário.

- - -
> ![Windows][Logo_Windows] Windows
>
> Em VMs do Windows está montada unidade temp Olá como unidade D:\ numa VM implementada.
>
> ![Linux][Logo_Linux] Linux
>
> Em VMs do Linux está montado como /mnt/resource ou /mnt. Consulte mais detalhes aqui:
>
> * [Como tooAttach tooa um disco de dados Máquina Virtual com Linux][virtual-machines-linux-how-to-attach-disk]
> * <http://blogs.msdn.com/b/mast/Archive/2013/12/07/Understanding-the-Temporary-drive-on-Windows-Azure-virtual-Machines.aspx>
>
>

- - -
unidade real Olá é volátil porque esta está a obter armazenada no servidor de anfitrião de Olá próprio. Se Olá VM moveu numa reimplementação (por exemplo, devida toomaintenance no anfitrião de Olá ou encerrar e reiniciar) Olá o conteúdo da unidade de Olá é perdido. Por conseguinte, não é uma opção toostore quaisquer dados importantes nesta unidade. tipo de Olá de suporte de dados utilizado para este tipo de armazenamento difere entre série VM diferente com as características de desempenho muito diferentes que, a partir de Junho de 2015, ter o seguinte aspeto:

* A5-A7: Muito limitado de desempenho. Não é recomendado para nada para além do ficheiro de paginação
* A8-A11: Características de desempenho muito bom com algumas IOPS dez thousand e > débito de 1GB por segundo.
* Série de D: Características de desempenho muito bom com algumas, em seguida, milhares de IOPS e > débito de 1GB por segundo.
* Série DS: Características de desempenho muito bom com algumas IOPS dez thousand e > débito de 1GB por segundo.
* Série de G: Características de desempenho muito bom com algumas IOPS dez thousand e > débito de 1GB por segundo.
* Série GS: Características de desempenho muito bom com algumas IOPS dez thousand e > débito de 1GB por segundo.

Aplicar os tipos VM toohello que são certificados com SAP declarações acima. Olá série da VM com excelente IOPS e débito se qualificam para tire partido por algumas funcionalidades DBMS. Consulte Olá [guia de implementação DBMS] [ dbms-guide] para obter mais detalhes.

Armazenamento do Microsoft Azure fornece persistentes de armazenamento e Olá típicos níveis de proteção e redundância visto no armazenamento SAN. Os discos com base no armazenamento do Azure estão disco rígido virtual (VHD) localizado nos serviços de armazenamento do Azure Olá. Olá disco de SO local (c Windows\, Linux / (dev/sda1)) é armazenado no Olá Storage do Azure e adicionais Volumes/discos montado toohello VM obter armazenados, demasiado.

É também possível tooupload um VHD existente no local ou criar campanhas vazias no Azure e anexar dessas VMs toodeployed. Os VHDs são referenciados como discos do Azure.

Depois de criar ou carregar um VHD para o armazenamento do Azure, é possível toomount e ligar esses tooan existente a Máquina Virtual e toocopy existente VHD (desmontado).

Como os VHDs são mantidos, dados e alterações naqueles são seguras quando a ser reiniciado e recriar uma instância de Máquina Virtual. Mesmo que uma instância é eliminada, estes VHDs permanecem seguros e podem voltar a implementar ou em caso de discos de SO não podem ser montado tooother VMs.

Dentro do Olá rede dos níveis de redundância diferente de armazenamento do Azure pode ser configurada:

* Nível mínimo que pode ser seleccionado é 'redundância local', o que é equivalente toothree-réplica dos dados de Olá dentro Olá mesmo centro de dados de uma região do Azure (consulte o capítulo [regiões do Azure][planning-guide-3.1]).
* Armazenamento com redundância de zona que serão distribuídas imagens Olá três através de centros de dados diferente dentro Olá mesma região do Azure.
* Nível de redundância de predefinido é redundância geográfica que replica de forma assíncrona conteúdo Olá outro imagens 3 dos dados de Olá para outra região do Azure que está alojado no Olá mesma região geopolítica.

Consulte também a tabela de Olá por cima deste artigo nas opções de redundância diferente do que diz respeito toohello: <https://azure.microsoft.com/pricing/details/storage/>

Mais informações no tooAzure que diz respeito que armazenamento pode ser encontrado aqui:

* <https://Azure.microsoft.com/Documentation/Services/Storage/>
* <https://Azure.microsoft.com/Services/site-Recovery>
* <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>
* <https://blogs.msdn.com/b/azuresecurity/Archive/2015/11/17/Azure-Disk-Encryption-for-Linux-and-Windows-virtual-Machines-Public-Preview.aspx>

#### <a name="azure-standard-storage"></a>Armazenamento padrão do Azure
Standard BLOB storage do Azure foi tipo Olá de armazenamento disponível quando foi lançada IaaS do Azure. Ocorreram quotas IOPS impostas por único VHD. Latência teve não estava a ser Olá mesma classe como dispositivos SAN/NAS normalmente implementados para sistemas SAP gama alta de classe alojada no local. Contudo, Olá armazenamento padrão do Azure foi tentativa suficiente para centenas de muitos sistemas SAP entretanto implementados no Azure.

Armazenamento padrão do Azure é cobrado com base no Olá real dados armazenados, volume de Olá de transações de armazenamento, transferências de dados de saída e opção de redundância escolhido. Podem ser criados vários VHDs em Olá máximo 1 TB de tamanho, mas, desde que os permanecerem vazios há sem qualquer encargo. Se, em seguida, de preencher um VHD com 100GB, será cobrada para 100GB de armazenamento e não para Olá de tamanho nominal Olá que VHD foi criado com.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Armazenamento Premium do Azure
Abril de 2015 Microsoft introduziu o Premium Storage do Azure. Armazenamento Premium foi introduzido com Olá objetivo tooprovide:

* Latência de e/s melhor.
* Melhorar o débito.
* Menor a variabilidade de latência de e/s.

Para essa finalidade, muitas das alterações foram introduzidas que Olá dois mais significativas são:

* Utilização de discos SSD em nós de armazenamento do Azure Olá
* Uma nova cache de leitura que é copiada por Olá SSD local de um nó de computação do Azure

Opposite armazenamento tooStandard onde capacidades não mudou depende do tamanho de Olá Olá disco (ou no VHD), Premium Storage atualmente tem 3 categorias de outro disco que são apresentadas no fim de Olá deste artigo antes de secção Olá FAQ: <https:/ /Azure.microsoft.com/pricing/details/Storage/>

Verá que são dependentes na categoria de tamanho de Olá dos discos de Olá IOPS/VHD e disco débito/VHD

Custo base no caso de Olá de armazenamento Premium não é o volume de dados real de Olá armazenado nessas VHDs, mas a categoria de tamanho de Olá de tal um VHD, independentemente da quantidade de Olá de dados de Olá armazenados em Olá VHD.

Também pode criar VHDs no armazenamento Premium que não são diretamente mapeamento em categorias de tamanho de Olá mostradas. Isto poderá ser o caso de Olá, especialmente quando copiar VHDs de armazenamento Standard para armazenamento Premium. Nestes casos, é efetuada uma mapeamento toohello seguinte maior armazenamento Premium opção de disco.

. Lembre-se de que apenas determinado série VM pode beneficiar do Olá Premium Storage do Azure. A partir de Dec de 2015, estes são Olá e GS-série DS. Olá-série DS é basicamente Olá mesmo como série D com a exceção de Olá que-série DS tem capacidade de Olá toomount armazenamento Premium baseadas em VMs adicionalmente tooVHDs que estão alojados no armazenamento padrão do Azure. Mesma coisa é válida para G-série em comparação comparada tooGS-série.

Se está a verificar saída Olá faz parte do Olá-série DS VMs no [neste artigo] [ virtual-machines-sizes] também irá tenha em atenção que existem limitações de volume de dados VHDs de armazenamento tooPremium na granularidade Olá de nível VM Olá. Série DS diferente ou série GS VMs também tem diferentes limitações que diz respeito toohello diversas os VHDs que podem ser montados. Estes limites estão documentados no artigo Olá mencionado acima, bem como. Mas essencialmente significa que se por exemplo, montar 32 tooa de discos/VHDs x P30 única DS14 VM não é possível obter 32 x débito máximo de Olá de um disco de P30. Em vez disso, hello débito máximo no nível VM, conforme documentado no artigo Olá irá limitar o débito de dados.

Obter mais informações sobre o armazenamento Premium podem ser encontradas aqui: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="azure-storage-accounts"></a>Contas de Armazenamento do Azure
Ao implementar os serviços ou VMs no Azure, implementação de VHDs e imagens da VM tem organizada em unidades denominadas contas do Storage do Azure. Ao planear uma implementação do Azure, terá de toocarefully considere restrições Olá do Azure. No lado Olá, há um número limitado de contas do Storage por subscrição do Azure. Apesar de cada conta de armazenamento do Azure pode conter um grande número de ficheiros VHD, há um limite fixo Olá total de IOPS por conta de armazenamento. Quando implementar centenas de SAP VMs com sistemas DBMS significativas de e/s de chamadas de criação, é recomendado toodistribute VMs de DBMS IOPS elevado entre várias contas do Storage do Azure. Deve ter cuidado não tooexceed Olá limite atual de contas do Storage do Azure por subscrição. Porque o armazenamento é uma parte vital da implementação de base de dados de Olá para um sistema SAP, este conceito é abordado mais detalhadamente na Olá já referenciada [guia de implementação DBMS][dbms-guide].

Podem encontrar mais informações sobre as contas de armazenamento do Azure no [neste artigo][storage-scalability-targets]. Ler este artigo, será tenha em atenção que existem diferenças de limitações Olá entre contas de armazenamento padrão do Azure e contas de armazenamento Premium. As principais diferenças são volume Olá dos dados que podem ser armazenados na conta do Storage. Armazenamento Standard volume Olá é um magnitude maior do que com o Premium Storage. No Olá outro Olá lado que gravemente é limitada a conta de armazenamento Standard IOPS (consulte a coluna 'Taxa Total de pedidos de'), ao passo que Olá conta de armazenamento do Azure Premium não tem nenhum desse limitação. Vamos abordar os detalhes e resultados destas diferenças quando debater implementações Olá dos sistemas SAP, especialmente servers do Olá DBMS.

Dentro de uma conta de armazenamento, terá de Olá possibilidade toocreate diferentes contentores objetivo Olá organizar e categorizar os VHDs diferentes. Estes contentores são tooe.g normalmente utilizados. Separe os VHDs de VMs diferentes. Não existem nenhum implicações de desempenho na utilização de apenas um contentor ou de vários contentores por baixo de uma única conta de armazenamento do Azure.

No Azure, um nome VHD segue Olá seguir uma ligação de nomenclatura tem de tooprovide um nome exclusivo para Olá VHD no Azure:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Como cadeia Olá mencionadas acima tem toouniquely identificar Olá VHD que é armazenado no Storage do Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Funcionamento em rede do Microsoft Azure
Microsoft Azure irá fornecer uma infraestrutura de rede que permite o mapeamento de Olá de todos os cenários que queremos toorealize com software SAP. capacidades de Olá são:

* Acesso a partir de Olá fora diretamente toohello VMs através de serviços de Terminal do Windows ou ssh/VNC
* Acesso tooservices e portas específicas utilizadas pelas aplicações dentro de Olá VMs
* Interno comunicação e resolução de nome entre um grupo de VMs implementadas como VMs do Azure
* Conectividade entre instalações, entre um cliente rede no local e Olá rede do Azure
* Cruzada região do Azure ou centro de dados conetividade entre sites do Azure

Podem encontrar mais informações aqui: <https://azure.microsoft.com/documentation/services/virtual-network/>

Existem muitos de nome de tooconfigure possibilidades diferentes e a resolução IP no Azure. Neste documento, apenas na nuvem cenários dependem predefinido Olá de utilizar o DNS do Azure (em contraste toodefining um serviço DNS próprio). Também é um novo serviço DNS do Azure que pode ser utilizado em vez de configurar o seu próprio servidor DNS. Podem encontrar mais informações no [neste artigo] [ virtual-networks-manage-dns-in-vnet] e no [nesta página](https://azure.microsoft.com/services/dns/).

Para cenários de vários locais que são a entidade confiadora no facto de Olá que Olá no local OpenLDAP/AD/DNS tiver sido expandido através de VPN ou tooAzure ligação privada. Determinados cenários conforme documentado aqui, poderá ser necessário toohave uma réplica de AD/OpenLDAP instalada no Azure.

Porque a rede e resolução de nomes é uma parte vital da implementação de base de dados de Olá para um sistema SAP, este conceito é abordado mais detalhadamente na Olá [guia de implementação DBMS][dbms-guide].

##### <a name="azure-virtual-networks"></a>Redes Virtuais do Azure
Através da criação de uma rede Virtual do Azure, pode definir o intervalo de endereços de Olá de endereços IP privados Olá atribuído por funcionalidade DHCP do Azure. Em cenários de vários locais, intervalo de endereços IP Olá definido ainda será atribuído utilizando o DHCP pelo Azure. No entanto, a resolução do nome de domínio irão ser efetuada no local (partindo do princípio de que as VMs de Olá fazem parte de um domínio no local) e, por conseguinte, pode resolver endereços para além dos diferentes serviços em nuvem do Azure.

[comment]: <> (MSSedusch continua a ser necessária? TODO originalmente uma Azure Virtual Network foi vinculada tooan grupo de afinidade. Com que uma rede Virtual no Azure obteve toohello restrito unidade de escala do Azure que Olá que obteve atribuir grupo de afinidade. No final de Olá, este Olá meant rede Virtual foi toohello restrito recursos disponíveis no Olá unidade de escala do Azure. Isto foi alterada desde e agora redes virtuais do Azure pode stretch em mais do que uma unidade de escala do Azure. No entanto, o que requer que as redes virtuais do Azure são * * não * * associados a grupos de afinidades já no momento de criação. Iremos já foi mencionado anteriormente que no oposta toorecommendations um ano há, deve * * não tirar partido dos grupos de afinidades do Azure já * *. Para obter mais informações, consulte < https://azure.microsoft.com/blog/regional-virtual-networks/>)

Cada máquina Virtual no Azure necessidades toobe ligado tooa rede Virtual.

Podem encontrar mais detalhes no [neste artigo] [ resource-groups-networking] e no [nesta página](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (Não foi TODO de MShermannd localizar um artigo que inclui o tópico de OpenLDAP Olá + ARM;)
[comment]: <> (MSSedusch < https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Por predefinição, depois de uma VM está implementada não é possível alterar a configuração de rede Virtual Olá. definições de TCP/IP Olá tem de ser deixadas toohello servidor de DHCP do Azure. Comportamento predefinido é a atribuição de IP dinâmico.
>
>

endereço de MAC Olá de placa de rede virtual Olá podem ser alterados por exemplo, depois de Windows novamente o tamanho e Olá ou SO de convidado Linux selecionará nova placa de rede Olá e irão utilizar automaticamente DHCP tooassign Olá endereços IP e DNS neste caso.

##### <a name="static-ip-assignment"></a>Atribuição de IP estático
É possível tooassign fixo ou endereços de IP reservado tooVMs dentro de uma rede Virtual do Azure. Olá VMs em execução numa rede Virtual do Azure é aberto um excelente possibilidade tooleverage esta funcionalidade, se necessário ou necessários para alguns cenários. atribuição de IP Olá permanece válida em toda a existência de Olá de Olá VM, independentemente da se Olá VM está em execução ou de encerramento. Como resultado, terá de tootake Olá número global de VMs (VMS em execução e paradas) em conta quando se definem Olá intervalo de endereços IP para Olá rede Virtual. endereço IP Olá permanecerá atribuído até Olá VM e respetiva Interface de rede é eliminado ou até que o endereço IP Olá anular obtém atribuído novamente. Consulte informações detalhadas no [neste artigo][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Vários NICs por VM
Pode definir várias placas de interface de rede virtual (vNIC) para uma máquina de Virtual do Azure. Com Olá capacidade toohave vNICs vários pode iniciar tooset segurança separação do tráfego de rede onde por exemplo, o tráfego de cliente é encaminhado através de um vNIC e back-end o tráfego é encaminhado através de um segundo vNIC. Dependente do tipo de Olá da VM, existem limitações diferentes regards toohello diversas vNICs. Podem encontrar detalhes exatos, funcionalidades e restrições nestes artigos:

* [Criar uma VM com vários NICs][virtual-networks-multiple-nics]
* [Implementar várias NIC VMs através de um modelo][virtual-network-deploy-multinic-arm-template]
* [Implementar várias NIC VMs com o PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Implementar várias NIC VMs utilizando Olá CLI do Azure][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Conetividade site a Site
Em vários locais é VMs do Azure e no local ligado com uma ligação de VPN transparente e permanente. É esperado toobecome Olá mais comuns SAP padrão de implementação no Azure. pressuposto Olá é que processos com instâncias SAP no Azure e de procedimentos operacionais deverão funcionar transparente. Isto significa que deve ser capaz de tooprint fora estes sistemas, bem como utilizar Olá tootransport de sistema de gestão de transporte de SAP (TMS) é alterado de um sistema de desenvolvimento no sistema de teste de tooa do Azure que é implementado no local. Pode encontrar mais documentação em torno do site para site na [neste artigo][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Dispositivo de túnel VPN
Ordenar toocreate uma ligação site a site (no local center tooAzure dados Centro de dados), terá de tooeither obter e configurar um dispositivo VPN ou utilizar o encaminhamento e acesso serviço remoto (RRAS) que foi introduzida como um componente de software com o Windows Server 2012.

* [Criar uma rede virtual com uma ligação de VPN de site para site com o PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [Acerca dos dispositivos VPN para ligações de Gateway de VPN de Site a Site][vpn-gateway-about-vpn-devices]
* [FAQ do VPN Gateway][vpn-gateway-vpn-faq]

![Ligação site a site entre no local e o Azure][planning-guide-figure-600]

Olá figura acima mostra duas subscrições do Azure tem subintervalos de endereço IP reservado para utilização em redes virtuais no Azure. conectividade de Olá de Olá no local tooAzure de rede é estabelecida através de VPN.

#### <a name="point-to-site-vpn"></a>VPN ponto a Site
VPN ponto a site requer que cada tooconnect de máquina do cliente com a respetiva VPN no Azure. Para cenários SAP Olá que está a visualizar, a conetividade ponto a site não é prática. Por conseguinte, não existem referências adicionais terá conectividade a VPN toopoint ao site.

[comment]: <> (MSSedusch - Obter mais informações podem ser encontradas aqui)
[comment]: <> (Ligação de TODO MShermannd já não é válido. Mas ARM ainda mesmo assim não suportado - consulte a seguinte hiperligação abaixo)
[comment]: <> (MSSedusch – < http://msdn.microsoft.com/library/azure/dn133798.aspx>.)
[comment]: <> (TooSite MShermannd TODO ponto ainda não suportado com ARM)
[comment]: <> (MSSedusch – < https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/>)

#### <a name="multi-site-vpn"></a>VPN multilocal
O Azure disponibiliza também nowadays Olá possibilidade toocreate VPN multilocal uma conectividade de uma subscrição do Azure. Uma única subscrição era anteriormente ligação de VPN de site para site tooone limitado. Esta limitação ausente correu com ligações de VPN multilocal para uma única subscrição. Isto torna possível tooleverage mais de uma região do Azure para uma subscrição específica através de configurações em vários locais.

Para obter mais documentação consulte [neste artigo][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO foi encontrada nenhuma ligação de docu ARM)

#### <a name="vnet-toovnet-connection"></a>VNet tooVNet ligação
Através da VPN multilocal, tem de tooconfigure uma rede Virtual do Azure separados em cada uma das regiões Olá. No entanto muito frequentemente tiver um requisito de Olá que componentes de software Olá em regiões diferentes Olá devem comunicar entre si. Idealmente, esta comunicação não deve ser encaminhada a partir de uma região do Azure tooon local e toohello há outra região do Azure. tooshortcut, o Azure disponibiliza Olá possibilidade tooconfigure uma ligação de uma rede Virtual do Azure no tooanother de região uma que Azure Virtual Network alojado noutra região. Esta funcionalidade é denominada ligação VNet a VNet. Obter mais detalhes sobre esta funcionalidade podem ser encontrados aqui: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>Privada ligação tooAzure – ExpressRoute
O Microsoft Azure ExpressRoute permite a criação de Olá de ligações privadas entre centros de dados do Azure e a infraestrutura no local de um cliente de Olá ou num ambiente de colocalização. ExpressRoute oferecido pelo MPLS vários fornecedores VPN (pacote de comutadores) ou de outros fornecedores de serviços de rede. As ligações do ExpressRoute não passam Olá Internet pública. As ligações ExpressRoute oferecem maior segurança, mais fiabilidade através de vários circuitos paralelos, velocidades mais rápidas e latências inferiores em relação a ligações típicas através de Olá Internet.

Encontrar mais detalhes sobre o ExpressRoute do Azure e ofertas aqui:

* <https://Azure.microsoft.com/Documentation/Services/expressroute/>
* <https://Azure.microsoft.com/pricing/details/expressroute/>
* <https://Azure.microsoft.com/Documentation/articles/expressroute-FAQs/>

Expressroute permite várias subscrições do Azure através de um circuito do ExpressRoute, conforme documentado aqui

* <https://Azure.microsoft.com/Documentation/articles/expressroute-howto-linkvnet-Arm/>
* <https://Azure.microsoft.com/Documentation/articles/expressroute-howto-circuit-Arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Imposição do túnel em caso de vários locais
Para VMs a associar a domínios no local através do site para site, ponto a site ou ExpressRoute, terá de certificar-se de que as definições de proxy de Internet Olá obter implementadas para todos os utilizadores de Olá dessas VMs, bem como toomake. Por predefinição, o software em execução nessas VMs ou utilizadores que utilizam um Olá de tooaccess browser internet não passará através do proxy de empresa Olá, mas seria ligar diretamente através do Azure toohello internet. Mas a definição de proxy de Olá, mesmo que não é um solução de 100% toodirect Olá o tráfego através do proxy de empresa Olá, uma vez que é responsabilidade do software e serviços toocheck para proxy de Olá. Se não está a ser fazer que software em execução no Olá VM ou um administrador manipula definições Olá, tráfego toohello Internet pode ser detoured novamente diretamente através do Azure toohello Internet.

Ordenar tooavoid isto, pode configurar a imposição do túnel com conectividade de site a site entre no local e o Azure. Olá descrição detalhada da funcionalidade da imposição do túnel Olá é publicada aqui <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Imposição de túnel com o ExpressRoute é ativado por clientes de publicidade uma rota predefinida através de Olá BGP de ExpressRoute sessões de peering.

#### <a name="summary-of-azure-networking"></a>Resumo de rede do Azure
Este capítulo continha muitos pontos importantes sobre redes do Azure. Eis um resumo dos pontos de principais de Olá:

* Redes virtuais do Azure permite tooset rede Olá, de acordo com tooyour suas próprias necessidades de cópia de segurança
* Redes virtuais do Azure pode ser tooVMs de intervalos de endereços IP aproveitadas tooassign ou atribuir tooVMs de endereços IP fixos
* tooset um Site para Site ou uma ligação ponto a Site, tem primeiro de toocreate uma Azure Virtual Network
* Assim que tiver sido implementada uma máquina virtual já não é Olá toochange possíveis que rede Virtual atribuído toohello VM

### <a name="quotas-in-azure-virtual-machine-services"></a>Quotas nos serviços de Máquina Virtual do Azure
Vamos precisar toobe limpar sobre facto Olá esse armazenamento Olá e infraestrutura de rede é partilhada entre VMs em execução uma variedade de serviços no Olá infraestrutura do Azure. E tal como em centros de dados do cliente de Olá, sobre-aprovisionar de alguns dos recursos de infraestrutura de Olá grau de tooa local. Olá plataforma Microsoft Azure utiliza o disco, a CPU, a rede e outros consumo de recursos do quotas toolimit Olá e toopreserve um desempenho consistente e determinística.  os tipos de VM diferentes Olá (A5 A6, etc.) ter diferentes quotas para o número de Olá de discos, CPU, RAM e da rede.

> [!NOTE]
> Recursos de CPU e memória dos tipos de VM de Olá suportados pelo SAP são pré-alocados em nós de anfitrião Olá. Isto significa que depois Olá VM é implementado, recursos de Olá no anfitrião de Olá estarão disponíveis como definido pelos Olá tipo VM.
>
>

Quando planear e dimensionar SAP soluções do Azure Olá quotas para cada tamanho da máquina virtual tem de ser considerada.  as quotas VM Olá descritas [aqui][virtual-machines-sizes].

quotas Olá descritas representam os valores de máximos teórico Olá.  limite de Olá de IOPS por VHD pode ser conseguido com o IOs pequenos (8kb), mas, possivelmente, não pode ser conseguido com o IOs grande (1Mb).  limite de IOPS Olá é aplicada a granularidade Olá de VHDs único.

Como um toodecide da árvore de decisão aproximada se um sistema SAP ajusta serviços de Máquina Virtual do Azure e as respetivas capacidades se necessita de um sistema existente toobe configurado de forma diferente no sistema de Olá toodeploy ordem no Azure, abaixo da árvore de decisões Olá pode ser utilizada ou:

![Decisão árvore toodecide capacidade toodeploy SAP no Azure][planning-guide-figure-700]

**Passo 1**: Olá toostart de informações mais importante com é o requisito de SAPS de Olá para um determinado sistema SAP. Olá SAPS requisitos necessidade toobe separada em parte do Olá DBMS e parte de aplicação de SAP Olá, mesmo se Olá sistema SAP já está implementado no local numa configuração de camada 2. Para sistemas existentes, Olá SAPS relacionados com hardware toohello em utilização, muitas vezes, pode ser determinado ou estimado com base nos testes de desempenho SAP existentes. resultados de Olá podem ser encontrados aqui: <http://global.sap.com/campaigns/benchmark/index.epx>.
Para sistemas SAP recentemente implementados, deve realizou um exercício de dimensionamento que deve determinar os requisitos de SAPS Olá do sistema de Olá.
Consulte também este blogue e o documento anexado para dimensionamento SAP no Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Passo 2**: para sistemas existentes, Olá volume de e/s e operações de e/s por segundo no servidor DBMS Olá devem ser medidas. Para sistemas recentemente planeados, Olá dimensionamento exercício para o novo sistema de Olá também deverá dar-ideias aproximadas dos requisitos de e/s de Olá no Olá lado DBMS. Se não souber, terá de eventualmente tooconduct uma prova de conceito.

**Passo 3**: requisito de SAPS Olá comparar para Olá server DBMS com Olá SAPS Olá VM tipos diferentes de Azure pode fornecer. informações de Olá no SAPS de diferentes tipos de VM do Azure Olá estão documentadas na nota SAP [1928533]. o foco de Olá deve estar num Olá DBMS VM pela primeira vez, uma vez que a camada de base de dados Olá camada Olá num sistema de SAP NetWeaver ampliar na maioria Olá das implementações. Em contrapartida, pode ser ampliada camada da aplicação Olá SAP. Se nenhum dos Olá SAP suportado tipos de VM do Azure podem proporcionar SAPS Olá necessária, não é possível executar a carga de trabalho Olá do sistema SAP Olá planeada no Azure. Terá ou toodeploy Olá sistema local ou terá de volume de carga de trabalho de Olá toochange para sistema Olá.

**Passo 4**: conforme documentado [aqui][virtual-machines-sizes], Azure impõe uma quota IOPS por independente VHD, se utilizar o armazenamento Standard ou Premium. Depende de Olá tipo VM, número de Olá de VHDs que podem ser montados varia. Como resultado, pode calcular um número IOPS máximo que pode ser conseguido com cada um dos tipos VM diferentes Olá. Depende de esquema do ficheiro de base de dados de Olá, pode stripe VHDs toobecome um volume no convidado Olá SO. No entanto, se Olá volume IOPS atual de um sistema SAP implementado excede os limites de Olá calculado Olá maior do tipo de VM do Azure e se não houver nenhuma toocompensate hipótese com mais memória, carga de trabalho de Olá de Olá sistema SAP pode gravemente afetada. Nestes casos, pode atingiu um ponto em que não deve implementar o sistema de Olá no Azure.

**Passo 5**: especialmente nos SAP sistemas que são implementados no local na camada 2 configurações, as possibilidades de Olá são que o sistema de Olá poderá ter toobe configurado no Azure numa configuração de 3 camadas. Neste passo, terá de toocheck se houver um componente na camada da aplicação de SAP Olá que não pode ser ampliada e que seria se ajusta Olá da CPU e memória recursos Olá diferentes oferta de tipos de VM do Azure. Se existir, de facto, um componente deste tipo, a carga de trabalho e de sistema SAP Olá não podem ser implementados no Azure. Mas se lhe pode escalável Olá aplicações SAP componentes em várias VMs do Azure, o sistema de Olá podem ser implementados no Azure.

**Passo 6**: se Olá DBMS e componentes da camada SAP aplicação podem ser executados em VMs do Azure, a configuração de Olá tem toobe definida com a:

* Número de VMs do Azure
* Tipos VM para componentes individuais Olá
* Número de VHDs em DBMS VM tooprovide suficiente IOPS

## <a name="managing-azure-assets"></a>Gerir recursos do Azure
### <a name="azure-portal"></a>Portal do Azure
Olá Portal do Azure é uma das três implementações de VM do Azure de toomanage interfaces. tarefas de gestão básico Olá, como implementar VMs a partir de imagens, podem ser feitas Olá Portal do Azure. Além disso, a criação de Olá de contas de armazenamento, redes virtuais e outros componentes do Azure também são Olá tarefas Portal do Azure pode processar muito bem. No entanto, funcionalidades como os VHDs a partir de carregamento no local tooAzure ou copiar um VHD no Azure são tarefas que necessitam de ferramentas de terceiros ou administração através do PowerShell ou a CLI.

![Portal do Microsoft Azure - descrição geral de Máquina Virtual][planning-guide-figure-800]

[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Tarefas de administração e a configuração para a instância de Máquina Virtual de Olá são possíveis a partir do Olá Portal do Azure.

Para além de reiniciar e encerrar uma Máquina Virtual também pode anexar, desanexar e criar discos de dados para a instância de Máquina Virtual de Olá, instância de Olá toocapture de preparação de imagem e configurar o tamanho da instância de Máquina Virtual de Olá Olá.

Olá Portal do Azure fornece funcionalidades básicas toodeploy e configurar as VMs e muitos outros serviços do Azure. No entanto não disponível funcionalidade é abrangida por Olá Portal do Azure. Olá Portal do Azure, não é possível tooperform tarefas, como:

* Carregar tooAzure de VHDs
* Copiar VMs

[comment]: <> (MShermannd TODO o sobre a automatização de serviço para SAP VMs?)
[comment]: <> (MSSedusch de implementação do SO de várias VMs entretanto possíveis)
[comment]: <> (MSSedusch também qualquer tipo de automatização relativas a implementação não é possível com Olá portal do Azure. Tarefas, tais como a implementação de script de várias VMs não é possível através de Olá Portal do Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Gestão através de cmdlets do PowerShell do Microsoft Azure
O Windows PowerShell é uma arquitetura de poderosa e extensível que foi amplamente ADOTOU pelos clientes implementar grandes quantidades de sistemas no Azure. Após a instalação de Olá de cmdlets do PowerShell num ambiente de trabalho, portáteis ou estação de gestão dedicado, Olá cmdlets do PowerShell pode ser executado remotamente.

Olá processo tooenable um ambiente de trabalho/portátil local para a utilização de Olá de cmdlets do PowerShell do Azure e como tooconfigure Olá os para utilização com Olá Azure subscrições é descrita no [neste artigo][powershell-install-configure].

Passos mais detalhados sobre como tooinstall, atualizar e configurar os cmdlets do Azure PowerShell Olá também podem ser encontrados na [este capítulo do guia de implementação de Olá][deployment-guide-4.1].

Experiência do cliente até ao momento foi PowerShell (PS) é certamente hello mais poderoso ferramenta toodeploy VMs e os passos toocreate personalizado na implementação de Olá de VMs. Todos os clientes de Olá executar instâncias SAP no Azure estão a utilizar tarefas de gestão de toosupplement do PS cmdlets não no Portal do Azure de Olá nem ainda estiver a utilizar cmdlets de PS exclusivamente toomanage as respetivas implementações no Azure. Uma vez que a partilha de cmdlets específicos do Azure Olá hello mesma Convenção de nomenclatura como Olá mais de 2000 cmdlets relacionados do Windows, é uma fácil de tarefas para Windows administradores tooleverage esses cmdlets.

Consulte o exemplo aqui: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO descrevem novos comandos da CLI quando testado)
Implementação de Olá extensão de monitorização do Azure para SAP (consulte o capítulo [solução de monitorização do Azure para SAP] [ planning-guide-9.1] neste documento) só é possível através do PowerShell ou a CLI. Por conseguinte, é obrigatório toosetup e configurar o PowerShell ou o CLI ao implementar ou administrar um sistema de SAP NetWeaver no Azure.  

Como o Azure oferece uma funcionalidade mais, novos cmdlets de PS vai toobe adicionado que necessita de uma atualização de Olá cmdlets. Por conseguinte faz Olá de toocheck sentido transferir o Azure site, pelo menos, uma vez mês de Olá <https://azure.microsoft.com/downloads/> para uma nova versão do Olá cmdlets. por cima da versão mais antiga Olá apenas será instalada a versão nova do Olá.

Para obter uma lista geral do Azure relacionados com comandos do PowerShell verifique aqui: <https://msdn.microsoft.com/library/azure/dn708514.aspx>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Gestão através de comandos da CLI do Microsoft Azure
Para os clientes que utilizam o Linux e pretendem toomanage Azure recursos Powershell poderão não ser uma opção. A Microsoft oferece o CLI do Azure como alternativa.
Olá CLI do Azure fornece um conjunto de código aberto, comandos de várias plataformas para trabalhar com Olá plataforma Azure. Olá CLI do Azure fornece muito Olá mesma funcionalidade encontrada no Olá portal do Azure.

Para obter informações sobre a instalação, configuração e como toouse CLI comandos tooaccomplish ver tarefas do Azure

* [Instalar Olá CLI do Azure][xplat-cli]
* [Implementar e gerir máquinas virtuais utilizando modelos Azure Resource Manager e Olá CLI do Azure][virtual-machines-linux-cli-deploy-templates]
* [Utilizar Olá CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager][xplat-cli-azure-resource-manager]

Leia também capítulo [CLI do Azure para VMs com Linux] [ deployment-guide-4.5.2] no Olá [guia de implementação] [ planning-guide] no como toouse CLI do Azure toodeploy hello do Azure Extensão de monitorização para SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Diferentes formas toodeploy VMs para SAP no Azure
Este capítulo ficará a saber toodeploy de formas diferentes de Olá uma VM no Azure. Procedimentos de preparação adicional, bem como o processamento de VHDs e as VMs do Azure é abrangidos neste capítulo.

### <a name="deployment-of-vms-for-sap"></a>Implementação de VMs para SAP
Microsoft Azure oferece várias formas toodeploy VMs e discos associados. Deste modo, é diferenças de Olá toounderstand muito importante, uma vez que os preparativos de VMs de Olá poderão diferir consoante o método Olá de implementação. Em geral, podemos irá observe Olá os seguintes cenários:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Mover uma VM de tooAzure no local com um disco não generalizado
Planear toomove um sistema específico de SAP da tooAzure no local. Isto pode ser feito através do carregamento Olá VHD que contém Olá SO, Olá binários SAP binários e DBMS plus Olá VHDs com dados Olá e ficheiros de Olá DBMS tooAzure de registo. Em contrapartida demasiado[cenário &#2; abaixo][planning-guide-5.1.2], mantenha o nome de anfitrião do Olá, SAP SID e contas de utilizador SAP Olá VM do Azure, tal como que foram configurados no ambiente no local de Olá. Por conseguinte, generalizar imagem Olá não é necessário. Consulte capítulos [preparação para mover uma VM de tooAzure no local com um disco não generalizado] [ planning-guide-5.2.1] deste documento para obter passos de preparação no local e o carregamento de VMs não generalizado ou VHDs tooAzure. Leia o capítulo [cenário 3: mover uma VM no local através de um VHD de Azure não generalizado com SAP] [ deployment-guide-3.4] no Olá [guia de implementação] [ deployment-guide]para obter passos detalhados de implementar essa uma imagem no Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Implementar uma VM com uma imagem específica do cliente
Devido a requisitos de patch de toospecific da sua versão do SO ou DBMS, imagens de Olá fornecido na Olá Azure Marketplace podem não atender as suas necessidades. Por conseguinte, poderá ser necessário toocreate uma VM utilizando a sua própria imagem de VM de SO/DBMS 'private' que pode ser implementada várias vezes posteriormente. uma imagem 'private' duplicação tooprepare, Olá seguintes itens ter toobe considerado:


[comment]: <> (MSSedusch > ver mais detalhes aqui:)
[comment]: <> (TAREFAS de MShermannd primeira ligação está sobre o modelo clássico. Não foi encontrado um artigo docu do Azure)
[comment]: <> (MSSedusch >< https://azure.microsoft.com/documentation/articles/virtual-machines-create-upload-vhd-windows-server/>)
[comment]: <> (MSSedusch >< http://blogs.technet.com/b/blainbar/archive/2014/09/12/modernizing-your-infrastructure-with-hybrid-cloud-using-custom-vm-images-and-resource-groups-in-microsoft-azure-part-21-blain-barton.aspx>)
- - -
> ![Windows][Logo_Windows] Windows
>
> Olá Windows definições (como o SID do Windows e o nome de anfitrião) devem ser abstracted/generalizado no Olá no local VM através do comando de sysprep Olá.
>
>
> ![Linux][Logo_Linux] Linux
>
> Siga os passos de Olá descritos nestes artigos para [SUSE] [ virtual-machines-linux-create-upload-vhd-suse] ou [Red Hat] [ virtual-machines-linux-redhat-create-upload-vhd] tooprepare toobe um VHD carregado tooAzure.
>
>

- - -
Se já tiver instalado o conteúdo SAP na VM no local (especialmente para sistemas de camada 2), pode adaptar as definições do sistema SAP Olá após a implementação de Olá de Olá VM do Azure através de instância de Olá mudar o nome de procedimento suportado pelo Olá SAP aprovisionamento de Software Gestor (nota SAP [1619720]). Consulte capítulos [preparação para implementar uma VM com uma imagem específica do cliente para SAP] [ planning-guide-5.2.2] e [carregar um VHD do local tooAzure] [ planning-guide-5.3.2]deste documento para obter passos de preparação no local e o carregamento de um generalizado tooAzure VM. Leia o capítulo [cenário 2: implementar uma VM com uma imagem personalizada para SAP] [ deployment-guide-3.3] no Olá [guia de implementação] [ deployment-guide] para obter passos detalhados de implementar essa uma imagem no Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Implementar uma VM fora Olá Azure Marketplace
Gostaria de toouse um Microsoft ou terceiros 3rd fornecidos imagem de VM de Olá Azure Marketplace toodeploy a VM. Depois de implementar a VM no Azure, siga Olá mesmas diretrizes e as ferramentas tooinstall Olá SAP software e/ou DBMS no interior da sua VM, tal como teria num ambiente no local. Para obter mais descrição da implementação, consulte capítulo [cenário 1: implementar uma VM fora Olá Azure Marketplace para SAP] [ deployment-guide-3.2] no Olá [guia de implementação] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Preparar as VMs com SAP para o Azure
Antes de carregar as VMs no Azure, é necessário toomake se Olá VMs e VHDs satisfazer determinados requisitos. Existem pequenas diferenças, dependendo do método de implementação de Olá que é utilizado.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Preparação para mover uma VM de tooAzure no local com um disco não generalizado
Um método de implementação comum é toomove uma VM existente que é executado um sistema SAP da tooAzure no local. Que VM Olá sistema SAP Olá VM apenas deve ser executada no Azure com Olá o mesmo nome de anfitrião e muito provavelmente Olá mesmo SAP SID. Neste caso Olá SO de VM convidado não deve ser generalizado para múltiplas implementações. Se a rede no local de Olá foi expandido para o Azure (consulte o capítulo [em vários locais - implementação única ou várias VMs SAP no Azure com o requisito de Olá de que está a ser totalmente integrados em rede no local de Olá] [ planning-guide-2.2] neste documento), em seguida, mesmo Olá mesmas contas de domínio podem ser utilizadas dentro de Olá VM os quais foram utilizados antes no local.

Requisitos ao preparar o seu próprio disco da VM do Azure são:

* Originalmente Olá VHD que contêm Olá sistema podem ter um tamanho máximo de 127GB apenas. Esta limitação foi eliminada no fim de Olá de Março de 2015. Agora hello VHD que contém o sistema de operativo Olá pode ser segurança too1TB tamanho como qualquer outro armazenamento do Azure alojada VHD, bem como.

[comment]: <> (MShermannd TODO ter toocheck se CLI também converte toostatic)
* Tem de toobe no Olá fixo formato VHD. Dinâmica VHDs ou VHDs no formato VHDx não são suportados ainda no Azure. Os VHDs dinâmicos será convertida toostatic VHDs ao carregar Olá VHD com o PowerShell mini-comandos ou a CLI
* VHDs que estão montado toohello VM e devem ser montados novamente no Azure toohello VM necessidade toobe um formato de VHD fixo. Olá mesmo limite de tamanho de disco do SO Olá aplica-se toodata discos bem. Os VHDs podem ter um tamanho máximo de 1TB. Os VHDs dinâmicos será convertida toostatic VHDs ao carregar Olá VHD com o PowerShell mini-comandos ou a CLI
* Adicione outra conta local com privilégios de administrador que pode ser utilizado pelo suporte da Microsoft ou que podem ser atribuídos como contexto de serviços e aplicações toorun no até Olá que implementação da VM e os utilizadores mais adequados pode ser utilizada.
* Para Olá maiúsculas e minúsculas de utilizar um cenário de implementação apenas de nuvem (consulte o capítulo [apenas na nuvem - implementações de Máquina Virtual no Azure sem dependências no Olá no local rede cliente] [ planning-guide-2.1] deste o documento) em combinação com este método de implementação, o domínio contas poderão não funcionar depois de Olá do disco do Azure estiver implementado no Azure. Isto é particularmente verdadeiro para as contas que são utilizados toorun serviços como o Olá DBMS ou SAP aplicações. Assim que precisa tooreplace essas contas de domínio com contas locais da VM e eliminar contas de domínio no local Olá no Olá VM. Manter os utilizadores de domínio no local na imagem de VM Olá não é um problema ao hello VM é implementado num cenário de Olá em vários locais, conforme descrito em capítulo [em vários locais - implementação única ou várias VMs SAP no Azure com o requisito de Olá ser totalmente integrado na rede no local de Olá] [ planning-guide-2.2] neste documento.
* Se foram utilizadas contas de domínio como inícios de sessão DBMS ou os utilizadores quando em execução nessas VMs e Olá sistema no local são supostos toobe implementado em cenários de apenas na nuvem, os utilizadores de domínio Olá necessitam toobe eliminado. É necessário toomake se de que o se administrador local Olá plus outro utilizador local de VM é adicionado como um início de sessão/utilizador Olá DBMS como administradores.
* Adicione outras contas locais como aqueles podem ser necessários para o cenário de implementação específico Olá.

- - -
> ![Windows][Logo_Windows] Windows
>
> Este cenário não generalização (sysprep) de Olá VM é tooupload necessário e implementar Olá VM no Azure.
> Certifique-se que unidade D:\ não é utilizado automount de disco do conjunto de discos ligados, conforme descrito em capítulo [definição automount para discos ligados] [ planning-guide-5.5.3] neste documento.
>
> ![Linux][Logo_Linux] Linux
>
> Este cenário não generalização (waagent-deprovision) de Olá VM é tooupload necessário e implementar Olá VM no Azure.
> Certifique-se de que o recurso/mnt/não é utilizado e que todos os discos estão montados através do uuid. Para o disco de SO de Olá Certifique-se de que a entrada de bootloader Olá reflete também a montagem de com base em uuid Olá.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Preparação para implementar uma VM com uma imagem específica do cliente para SAP
Ficheiros VHD que contêm um SO generalizado também são armazenados nos contentores nas contas de armazenamento do Azure. Pode implementar uma nova VM a partir de uma imagem VHD consultando Olá VHD como uma origem de VHD nos seus ficheiros de modelo de implementação, conforme descrito em capítulo [cenário 2: implementar uma VM com uma imagem personalizada para SAP] [ deployment-guide-3.3] de Olá [Guia de implementação][deployment-guide].

Requisitos quando preparar a sua própria imagem de VM do Azure são:

* Originalmente Olá VHD que contêm Olá sistema podem ter um tamanho máximo de 127GB apenas. Esta limitação foi eliminada no fim de Olá de Março de 2015. Agora hello VHD que contém o sistema de operativo Olá pode ser segurança too1TB tamanho como qualquer outro armazenamento do Azure alojada VHD, bem como.

[comment]: <> (MShermannd TODO ter toocheck se CLI também converte toostatic)
* Tem de toobe no Olá fixo formato VHD. Dinâmica VHDs ou VHDs no formato VHDx não são suportados ainda no Azure. Os VHDs dinâmicos será convertida toostatic VHDs ao carregar Olá VHD com o PowerShell mini-comandos ou a CLI
* VHDs que estão montado toohello VM e devem ser montados novamente no Azure toohello VM necessidade toobe um formato de VHD fixo. Olá mesmo limite de tamanho de disco do SO Olá aplica-se toodata discos bem. Os VHDs podem ter um tamanho máximo de 1TB. Os VHDs dinâmicos será convertida toostatic VHDs ao carregar Olá VHD com o PowerShell mini-comandos ou a CLI
* Uma vez que todos os utilizadores de domínio registados como não existem utilizadores Olá VM num cenário apenas na nuvem de Olá (consulte o capítulo [apenas na nuvem - implementações de Máquina Virtual no Azure sem dependências no Olá no local rede cliente] [ planning-guide-2.1] deste documento), serviços, utilizar esse domínio contas poderão não funcionar depois de Olá imagem é implementado no Azure. Isto é particularmente verdadeiro para as contas que são utilizados toorun serviços como o DBMS ou SAP aplicações. Assim que precisa tooreplace essas contas de domínio com contas locais da VM e eliminar contas de domínio no local Olá no Olá VM. Manter os utilizadores de domínio no local na imagem de VM Olá poderão não ser um problema quando Olá VM for implementada num Olá em vários locais cenário conforme descrito em capítulo [em vários locais - implementação única ou várias VMs SAP no Azure com o requisito de Olá de a ser totalmente integrados em rede no local de Olá] [ planning-guide-2.2] neste documento.
* Adicione outra conta local com privilégios de administrador que pode ser utilizado pelo suporte da Microsoft nas investigações de problema ou que podem ser atribuídos como contexto de serviços e aplicações toorun no até Olá que implementação da VM e os utilizadores mais adequados pode ser utilizada.
* Em implementações apenas na nuvem e em que foram utilizadas contas de domínio como inícios de sessão DBMS ou os utilizadores quando em execução Olá sistema no local, os utilizadores de domínio Olá devem ser eliminados. Tem de certificar-se de que o administrador local Olá plus outro utilizador local de VM é adicionado como um utilizador/início de sessão do Olá DBMS como administradores toomake.
* Adicione outras contas locais como aqueles podem ser necessários para o cenário de implementação específico Olá.
* Se a imagem de Olá contém uma instalação do SAP NetWeaver e mudar o nome do nome de anfitrião Olá do nome original do Olá momento Olá de Olá implementação do Azure, é provável que, é recomendado toocopy Olá versões mais recentes do DVD de Gestor de aprovisionamento de Software do SAP Olá em modelo de Olá. Isto permitirá tooeasily utilize Olá SAP fornecido a mudança de nome funcionalidade tooadapt Olá alterado hostname e/ou alterar Olá SID do Olá sistema SAP dentro Olá implementado imagem de VM, assim que uma nova cópia é iniciada.

- - -
> ![Windows][Logo_Windows] Windows
>
> Certifique-se que unidade D:\ não é utilizado automount de disco do conjunto de discos ligados, conforme descrito em capítulo [definição automount para discos ligados] [ planning-guide-5.5.3] neste documento.
>
> ![Linux][Logo_Linux] Linux
>
> Certifique-se de que o recurso/mnt/não é utilizado e que todos os discos estão montados através do uuid. Para Olá SO disco certificar entrada de bootloader Olá também reflete a montagem de com base em uuid Olá.
>
>

- - -
* GUI de SAP (para administrativas e fins do programa de configuração) podem ser instalados previamente nesse modelo.
* Mudar o nome de outro software necessário toorun Olá VMs com êxito em cenários de vários locais pode ser instalado, desde que este software pode trabalhar com Olá de Olá VM.

Se Olá VM está preparado suficientemente toobe genérico e, eventualmente, independentemente de contas/utilizadores não está disponíveis no Olá direcionada cenário de implementação do Azure, é efetuado Olá último preparação passo do generalizar essa uma imagem.

##### <a name="generalizing-a-vm"></a>Generalizar uma VM
- - -
[comment]: <> (MShermannd TODO tiver artigos melhores toofind / docu sobre generalizar Olá VMs para ARM)
> ![Windows][Logo_Windows] Windows
>
> último passo de Olá é toolog no tooa VM com uma conta de administrador. Abra uma janela de comandos do Windows como 'Administrador'. Aceda too...\windows\system32\sysprep e executar sysprep.exe.
> Será apresentada uma janela de pequena. É importante toocheck Olá 'Generalize' opção (a predefinição de Olá é anular marcada) e altere Olá opção de encerramento de predefinido de too'Shutdown 'Reiniciar' '. Este procedimento assume que o processo de sysprep Olá é executado no local na Olá SO convidado de uma VM.
> Se quiser procedimento de Olá tooperform com uma VM já em execução no Azure, siga os passos de Olá descritos nos [neste artigo][virtual-machines-windows-capture-image].
>
> ![Linux][Logo_Linux] Linux
>
> [Como toocapture um toouse de máquina virtual Linux como um modelo do Resource Manager][virtual-machines-linux-capture-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Transferência de VMs e VHDs entre tooAzure no local
Uma vez que o carregamento tooAzure de imagens e os discos VM não é possível através de Olá Portal do Azure, terá de cmdlets do Azure PowerShell toouse ou a CLI. Possibilidade de outra é a utilização de Olá da ferramenta de Olá 'AzCopy'. ferramenta de Olá pode copiar VHDs entre no local e o Azure (em ambas as direções). Também pode copiar VHDs entre regiões do Azure. Consulte [esta documentação] [ storage-use-azcopy] para transferência e utilização do AzCopy.

Uma terceira alternativa seria toouse várias ferramentas de GUI orientado para terceiros. No entanto, certifique-se que estas ferramentas são que suportam Blobs de páginas do Azure. Para armazenam o nosso fins precisamos toouse Blob de página do Azure (diferenças Olá são descritas aqui: <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>). Também ferramentas de Olá fornecidas pelo Azure são muito eficientes no compressão Olá VMs e os VHDs que precisam toobe carregado. Isto é importante porque esta eficiência na compressão reduz o tempo de carregamento de Olá (que varia mesmo assim consoante toohello de ligação de carregamento de Olá internet a partir das instalações do Olá no local e a região de implementação do Azure Olá visados). É um justa pressuposto que carregar uma VM ou o VHD da localização alfabetos toohello E.U.A. com base em dados do Azure centros irão demorar mais do que o carregamento Olá mesmos centros de dados do Azure que toohello VMs/VHDs.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Carregar um VHD do tooAzure no local
tooupload uma VM existente ou um VHD do Olá no local de uma VM de rede ou o VHD tem dos requisitos de Olá toomeet conforme indicado em capítulo [preparação para mover uma VM de tooAzure no local com um disco não generalizado] [ planning-guide-5.2.1] deste documento.

Este tipo uma VM não precisa de toobe generalizado e pode ser também carregada num Estado de Olá e forma tem após o encerramento em Olá no local do lado do. Olá mesmo se aplica VHDs adicionais que não contém qualquer sistema operativo.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Carregar um VHD e tornando-a um disco do Azure
Neste caso, iremos pretende tooupload um VHD, com ou sem sistema operativo no mesmo e montá-la tooa VM como um disco de dados ou utilizá-lo como disco do SO. Este é um processo de vários passo

**PowerShell**

* Subscrição de tooyour de início de sessão com *Login-AzureRmAccount*
* Definir Olá subscrição do seu contexto com *Set-AzureRmContext* e SubscriptionId de parâmetro ou SubscriptionName - consulte <https://msdn.microsoft.com/library/mt619263.aspx>
* Carregar Olá VHD com *adicionar AzureRmVhd* tooan conta do Storage do Azure - consulte <https://msdn.microsoft.com/library/mt603554.aspx>
* Disco de Olá SO de conjunto de uma nova toohello de configuração VM VHD com *conjunto AzureRmVMOSDisk* -consulte <https://msdn.microsoft.com/library/mt603746.aspx>
* Criar uma nova VM a partir da configuração VM Olá com *New-AzureRmVM* -consulte <https://msdn.microsoft.com/library/mt603754.aspx>
* Adicionar um tooa de disco de dados nova VM com *adicionar AzureRmVMDataDisk* -consulte <https://msdn.microsoft.com/library/mt603673.aspx>

**CLI do Azure**

* Modo de Gestor de recursos do comutador tooAzure com *arm do modo de configuração do azure*
* Subscrição de tooyour de início de sessão com *início de sessão do azure*
* Selecione a sua subscrição com *conjunto da conta do azure`<subscription name or id`>*
* Carregar Olá VHD com *carregamento do blob storage do azure* -consulte [Using Olá CLI do Azure com o Storage do Azure][storage-azure-cli]
* Criar uma nova VM Olá carregados VHD como disco de SO com a especificação *vm do azure crie* e o parâmetro -d
* Adicionar um tooa de disco de dados nova VM com *vm disco anexar novo*

**Modelo**

* Carregar Olá VHD com o Powershell ou a CLI do Azure
* Implementar Olá VM com um modelo JSON referenciar Olá VHD, conforme mostrado no [este modelo JSON de exemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-from-specialized-vhd/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Implementação de uma imagem VM
tooupload uma VM existente ou um VHD do Olá no local de rede na ordem toouse-la como uma imagem de VM do Azure tal uma VM ou VHD tem dos requisitos de Olá toomeet listados no capítulo [preparação para implementar uma VM com uma imagem específica do cliente para SAP] [ planning-guide-5.2.2] deste documento.

* Utilize *sysprep* no Windows ou *waagent-deprovision* no Linux toogeneralize o VM - consulte [como toocapture uma máquina virtual do Windows no Olá implementação do Resource Manager modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture um toouse de máquina virtual Linux como um modelo do Resource Manager][virtual-machines-linux-capture-image-capture]
* Subscrição de tooyour de início de sessão com *Login-AzureRmAccount*
* Definir Olá subscrição do seu contexto com *Set-AzureRmContext* e SubscriptionId de parâmetro ou SubscriptionName - consulte <https://msdn.microsoft.com/library/mt619263.aspx>
* Carregar Olá VHD com *adicionar AzureRmVhd* tooan conta do Storage do Azure - consulte <https://msdn.microsoft.com/library/mt603554.aspx>
* Disco de Olá SO de conjunto de uma nova toohello de configuração VM VHD com *Set AzureRmVMOSDisk - SourceImageUri - CreateOption fromImage* -consulte <https://msdn.microsoft.com/library/mt603746.aspx>
* Criar uma nova VM a partir da configuração VM Olá com *New-AzureRmVM* -consulte <https://msdn.microsoft.com/library/mt603754.aspx>

**CLI do Azure**

* Utilize *sysprep* no Windows ou *waagent-deprovision* no Linux toogeneralize o VM - consulte [como toocapture uma máquina virtual do Windows no Olá implementação do Resource Manager modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture um toouse de máquina virtual Linux como um modelo do Resource Manager] [ virtual-machines-linux-capture-image-capture] para Linux
* Modo de Gestor de recursos do comutador tooAzure com *arm do modo de configuração do azure*
* Subscrição de tooyour de início de sessão com *início de sessão do azure*
* Selecione a sua subscrição com *conjunto da conta do azure`<subscription name or id`>*
* Carregar Olá VHD com *carregamento do blob storage do azure* -consulte [Using Olá CLI do Azure com o Storage do Azure][storage-azure-cli]
* Criar uma nova VM Olá carregados VHD como disco de SO com a especificação *vm do azure crie* e o parâmetro -Q

**Modelo**

* Utilize *sysprep* no Windows ou *waagent-deprovision* no Linux toogeneralize o VM - consulte [como toocapture uma máquina virtual do Windows no Olá implementação do Resource Manager modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture um toouse de máquina virtual Linux como um modelo do Resource Manager] [ virtual-machines-linux-capture-image-capture] para Linux
* Carregar Olá VHD com o Powershell ou a CLI do Azure
* Implementar Olá VM com um modelo JSON, conforme mostrado na imagem Olá VHD a referenciar [este modelo JSON de exemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-tooon-premises"></a>Transferir VHDs tooon local
Infraestrutura do Azure como um serviço não é uma rua unidirecional apenas ser capaz de tooupload VHDs e sistemas SAP. Pode mover SAP sistemas a partir do Azure novamente para o Olá, mundo no local, bem como.

Durante a hora de Olá da transferência Olá Olá VHDs não pode ser Active Directory. Mesmo quando transferir os VHDs que estão montados tooVMs, Olá VM tem toobe encerramento. Ainda pode estar operacional se apenas pretender toodownload Olá base de dados de conteúdo que, em seguida, deve ser utilizado tooset configurar um novo sistema no local e se é aceitável que durante a hora Olá Olá transferir e Olá a configuração do sistema de nova Olá que Olá sistema no Azure , pode evitar um longo período de inatividade, efetuando uma cópia de segurança da base de dados comprimido para um VHD e transferir apenas que o VHD em vez de transferirem também Olá VM base do SO.

#### <a name="powershell"></a>PowerShell
Depois de sistema SAP Olá está parado e Olá VM for encerrado, pode utilizar o cmdlet do PowerShell Olá AzureRmVhd guardar no Olá no local fazer uma cópia de discos VHD do destino toodownload Olá mundo do toohello no local. Toodo, é necessário Olá URL de Olá VHD que pode encontrar no Olá 'Armazenamento secção' de Olá Portal do Azure (necessidade toonavigate toohello conta de armazenamento e Olá contentor de armazenamento onde hello VHD foi criado) e terá de tooknow onde hello VHD deve ser copiar para.

Em seguida, pode tirar partido do comando de Olá definindo simplesmente parâmetro Olá SourceUri como URL Olá de toodownload VHD Olá e Olá LocalFilePath como localização física do Olá de Olá VHD (incluindo o respetivo nome). comando Olá pode ter o seguinte aspeto:

```powerhell
Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
```

Para mais detalhes sobre o cmdlet Olá AzureRmVhd guardar, verifique aqui <https://msdn.microsoft.com/library/mt622705.aspx>.

#### <a name="cli"></a>CLI
Depois de sistema SAP Olá está parado e Olá VM for encerrado, pode utilizar transferência blob storage do azure de comando de CLI do Azure de Olá no Olá no local fazer uma cópia de discos VHD do destino toodownload Olá mundo do toohello no local. Toodo que, terá de nome de Olá e contentor Olá Olá VHD que pode encontrar no Olá 'Armazenamento secção' de Olá Portal do Azure (necessidade toonavigate toohello conta de armazenamento e Olá contentor de armazenamento onde hello VHD foi criado) e terá de tooknow onde Olá VHD deve ser copiado para.

Em seguida, pode tirar partido do comando de Olá definindo simplesmente blob de parâmetros de Olá e contentor de toodownload VHD Olá e de destino Olá como localização de destino físico Olá de Olá VHD (incluindo o respetivo nome). comando Olá pode ter o seguinte aspeto:

```
azure storage blob download --blob <name of hello VHD toodownload> --container <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --destination <destination of hello VHD toodownload>
```

### <a name="transferring-vms-and-vhds-within-azure"></a>Transferência de VMs e VHDs no Azure
#### <a name="copying-sap-systems-within-azure"></a>Copiar sistemas SAP no Azure
Um sistema SAP ou mesmo DBMS servidor dedicado que suporta uma camada de aplicação do SAP será provavelmente consistem de vários VHDs que contêm o Olá SO com binários de Olá ou Olá dados e ficheiros do Olá SAP da base de dados de registo. Olá, Azure funcionalidade de copiar VHDs nem hello funcionalidade do Azure de guardar VHDs toodisk tem um mecanismo de sincronização que seria instantâneo vários VHDs forma síncrona. Por conseguinte, o estado de Olá de Olá copiados ou guardado VHDs, mesmo que se encontram estão montados contra Olá mesma VM seria diferente. Isto significa que Olá concreto maiúsculas e minúsculas de ter dados diferentes e logfile(s) contidas no Olá VHDs diferentes, Olá base de dados no final de Olá seria possível inconsistente.

**Conclusão: Na ordem toocopy ou guardar o VHD que fazem parte de uma configuração de sistema do SAP precisa toostop Olá SAP sistema e também precisa de tooshut baixo Olá implementado VM. Apenas, em seguida, pode copiar ou transferir Olá conjunto de VHDs tooeither criar uma cópia do sistema SAP Olá no Azure ou no local.**

Os discos de dados são armazenados como ficheiros VHD numa conta de armazenamento do Azure e podem ser diretamente anexar a máquina virtual de tooa ou ser utilizado como uma imagem. Neste caso, Olá VHD é copiado tooanother localização antes de beeing ligado toohello máquina. Olá nome completo do ficheiro VHD Olá no Azure tem de ser exclusivo no Azure. Tal como mencionado anteriormente já, o nome de Olá é tipos de um nome de três partes que se pareça com:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

##### <a name="powershell"></a>PowerShell
Pode utilizar o Azure PowerShell cmdlets toocopy um VHD conforme mostrado no [neste artigo][storage-powershell-guide-full-copy-vhd].

##### <a name="cli"></a>CLI
Pode utilizar CLI do Azure toocopy um VHD, conforme mostrado no [neste artigo][storage-azure-cli-copy-blobs]

##### <a name="azure-storage-tools"></a>Ferramentas de armazenamento do Azure
* <http://azurestorageexplorer.Codeplex.com/releases/View/125870>

Existem também edições professional do exploradores de armazenamento do Azure que pode ser encontrada aqui:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

cópia de Olá de um VHD próprio dentro de uma conta de armazenamento é um processo que demora apenas alguns segundos (tooSAN hardware semelhante a criação de instantâneos com cópia lento e copie na escrita). Depois de ter uma cópia do ficheiro VHD Olá pode anexar tooa máquinas de virtuais ou utilize-o como uma imagem tooattach copia das máquinas de toovirtual Olá VHD.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption fromImage
$vm | Update-AzureRmVM
```
##### <a name="cli"></a>CLI
```
azure config mode arm

# attach a vhd tooa vm
azure vm disk attach <resource group name> <vm name> <path toovhd>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Copiar os discos entre contas de armazenamento do Azure
Não é possível efetuar esta tarefa Olá Portal do Azure. Pode ise do PowerShell do Azure cmdlets, a CLI do Azure ou de terceiros terceiros armazenamento browser. Olá, os cmdlets do PowerShell ou os comandos da CLI podem criar e gerir blobs, que incluem os blobs de cópia do Olá capacidade tooasynchronously em contas de armazenamento e em regiões Olá subscrição do Azure.

##### <a name="powershell"></a>PowerShell
Também é possível copiar VHDs entre subscrições. Para obter mais informações, leia [neste artigo][storage-powershell-guide-full-copy-vhd].

fluxo básico de Olá de Olá lógica de cmdlet do PS tem o seguinte aspeto:

* Criar um contexto de conta de armazenamento para a conta de armazenamento de origem Olá com *New-AzureStorageContext* -consulte <https://msdn.microsoft.com/library/dn806380.aspx>
* Criar um contexto de conta de armazenamento para a conta de armazenamento de destino Olá com *New-AzureStorageContext* -consulte <https://msdn.microsoft.com/library/dn806380.aspx>
* Iniciar a cópia de Olá com

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Verificar o estado de Olá da cópia de Olá num ciclo com

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Anexe Olá nova VHD tooa máquina virtual, tal como descrito acima.

Para exemplos, consulte [neste artigo][storage-powershell-guide-full-copy-vhd]

##### <a name="cli"></a>CLI
* Iniciar a cópia de Olá com

```
  azure storage blob copy start --source-blob <source blob name> --source-container <source container name> --account-name <source storage account name> --account-key <source storage account key> --dest-container <target container name> --dest-blob <target blob name> --dest-account-name <target storage account name> --dest-account-key <target storage account name>
```

* Verificar o estado de Olá se hello cópia num ciclo com

```
azure storage blob copy show --blob <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Anexe Olá nova VHD tooa máquina virtual, tal como descrito acima.

Para exemplos, consulte [neste artigo][storage-azure-cli-copy-blobs]

### <a name="disk-handling"></a>Processamento de disco
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Estrutura do VM/VHD para as implementações de SAP
Idealmente Olá processamento da estrutura de Olá de uma VM e VHDs Olá associado devem ser muito simples. Nas instalações no local, os clientes desenvolveu várias formas de structuring uma instalação de servidor.

* Um VHD de base que contém Olá SO e todos os binários Olá Olá DBMS e/ou SAP. Desde Março de 2015, este VHD pode ser segurança too1TB tamanho em vez de restrições anteriores que limitada-too127GB.
* Um ou vários VHDs que contém Olá DBMS ficheiro de registo da base de dados do Olá SAP e ficheiro de registo de Olá de Olá área de armazenamento temp DBMS (se Olá DBMS suportar isto). Se os requisitos de IOPS de registo de base de dados de Olá estiverem elevados, terá de toostripe vários VHDs no volume IOPS ordem tooreach Olá necessário.
* Um número de VHDs que contém um ou dois ficheiros de base de dados da base de dados do Olá SAP Olá DBMS temp ficheiros de dados, bem como (se Olá DBMS suportar isto).

![Configuração de referência da VM do IaaS do Azure para SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO descrevem a estrutura do Linux)

- - -
> ![Windows][Logo_Windows] Windows
>
> Com muitos clientes vimos configurações onde, por exemplo, SAP e DBMS binários não foram instalados numa unidade c:\ de olá onde hello SO foi instalado. Ocorreram vários motivos para tal, mas quando vamos voltar correu toohello raiz, normalmente, foi que Olá unidades foram pequenas e as atualizações de SO necessário espaço adicional há a 10 a 15 anos. Ambas as condições não aplicam demasiado frequentemente já estes dias. Hoje em dia unidade c:\ de Olá pode ser mapeada em discos de grande volume ou VMs. Nas implementações de tookeep ordem simples na sua estrutura, é recomendado toofollow o padrão de implementação seguinte para sistemas de SAP NetWeaver no Azure
>
> ficheiro de paginação de sistema operativo de Windows de Olá deve estar num Olá unidade d: (não persistentes disco)
>
> ![Linux][Logo_Linux] Linux
>
> Coloque Olá Linux swapfile em recursos/mnt//mnt no Linux, conforme descrito em [neste artigo][virtual-machines-linux-agent-user-guide]. ficheiro de comutação Olá pode ser configurado no ficheiro de configuração de Olá de Olá /etc/waagent.conf agente Linux. Adicionar ou alterar Olá seguintes definições:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

alterações de Olá tooactivate, terá de toorestart Olá agente Linux com

```
sudo service waagent restart
```

Leia a nota SAP [1597355] para obter mais detalhes sobre Olá recomendado tamanho do ficheiro de troca

- - -
número de Olá de VHDs utilizada para os ficheiros de dados do Olá DBMS e tipo de Olá do Storage do Azure estes VHDs estão alojados no deve ser determinado pelos requisitos de IOPS de Olá e latência Olá necessário. Quotas exatas descritas [neste artigo][virtual-machines-sizes]

Experiência de implementações de SAP através de Olá últimos anos 2 taught-nos alguns lições que podem ser resumidas como:

* Ficheiros de dados de toodifferent de tráfego IOPS nem sempre é Olá iguais, uma vez que os sistemas de cliente existente poderão ter outro nome dado um tamanho dados ficheiros que representa as respetivas bases de dados SAP. Como resultado, acabou toobe melhor utilizando uma configuração do RAID através de vários VHDs tooplace Olá ficheiros de dados que LUNs carved fora dos. Ocorreram situações, especialmente com o armazenamento padrão do Azure onde uma taxa IOPS atingiu a quota de Olá de um único VHD contra o registo de transações de DBMS Olá. Em utilização Olá cenários de armazenamento Premium é recomendado ou em alternativa, Agregar vários VHDs de armazenamento Standard com um RAID de software.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Melhores práticas do desempenho para o SQL Server em Azure Virtual Machines][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Configurar Software RAID no Linux][virtual-machines-linux-configure-raid]
> * [Configurar LVM numa VM com Linux no Azure][virtual-machines-linux-configure-lvm]
> * [Os segredos de armazenamento do Azure e otimizações de e/s do Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Armazenamento Premium está a ser mostrada significativo um melhor desempenho, especialmente para gravações de registo de transação críticos. Para cenários SAP que são toodeliver esperado de produção, tais como desempenho, recomenda-se vivamente toouse série de VM que pode tirar partido do Premium Storage do Azure.

Tenha em atenção que Olá VHD que contém Olá SO e como recomendamos, Olá binários SAP e hello base de dados (base VM), já não faz too127GB limitado. Agora pode ter segurança too1TB de tamanho. Isto deve ser suficiente espaço tookeep Olá todos os ficheiros necessários, por exemplo, incluindo os registos da tarefa batch SAP.

Para mais sugestões e obter mais detalhes, especificamente para DBMS VMs, consulte Olá [DBMS guia de implementação][dbms-guide]

#### <a name="disk-handling"></a>Processamento de disco
Na maioria dos cenários terá toocreate discos adicionais na ordem toodeploy Olá SAP da base de dados para Olá VM. Falamos sobre as considerações de Olá no número de VHDs em capítulo [estrutura do VM/VHD para as implementações de SAP] [ planning-guide-5.5.1] deste documento. Olá Portal do Azure permite tooattach e desanexar os discos depois de uma VM base é implementada. discos de Olá podem estar em execução, bem como quando está parado e expor/anular a exposição quando Olá VM está a funcionar. Ao anexar um disco, Olá Portal do Azure oferece tooattach um disco vazio ou um disco existente, que, neste ponto no tempo não está ligado tooanother VM.

**Tenha em atenção**: VHDs só podem ser anexado tooone VM em qualquer momento.

![Anexar / desanexar os discos com o armazenamento padrão do Azure][planning-guide-figure-1400]

É necessário toodecide se pretende que toocreate um VHD de novo e vazio (que seria possível criar Olá a mesma conta de armazenamento como Olá base VM está a ser) ou se pretende tooselect um VHD existente que foi carregado anteriormente e deve ser ligado toohello VM agora.

**IMPORTANTE**: **fazer não** pretende toouse colocação em cache do anfitrião com o armazenamento padrão do Azure. Deve deixe preferência de Cache do anfitrião de Olá predefinido Olá de NONE. Com o Premium Storage do Azure deverá ativar a colocação em cache de leitura se uma característica das e/s de Olá principalmente é de leitura como o tráfego de e/s normal contra os ficheiros de dados de base de dados. Em caso de ficheiro de registo de transação de base de dados se recomenda a sem colocação em cache.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Olá, como tooattach dados de um disco no portal do Azure][virtual-machines-windows-attach-disk-portal]
>
> Se os discos estão anexados, terá de toolog para Olá de tooopen Olá VM Gestor de discos do Windows. Se não estiver ativada automount conforme recomendado nas capítulo [definição automount para discos ligados][planning-guide-5.5.3], hello volume anexado recentemente tem toobe colocado online e inicializar.
>
> ![Linux][Logo_Linux] Linux
>
> Se os discos estão anexados, terá toolog para Olá VM e inicializar discos Olá, conforme descrito em [neste artigo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Se o disco novo Olá é um disco vazio, é necessário, bem como o disco de Olá tooformat. Para a formatação, especialmente para DBMS ficheiros de registo e dados Olá mesmas recomendações relativamente às implementações bare-metal de Olá que DBMS aplicar.

Como já mencionados capítulo [Olá conceito de Máquina Virtual do Microsoft Azure][planning-guide-3.2], uma conta de armazenamento do Azure fornece os recursos infinito em termos de volume de e/s, volume de dados e de IOPS. Normalmente, DBMS VMs são mais afetados por este problema. Poderá ser melhor toouse uma conta de armazenamento separada para cada VM se tiver alguns toodeploy de VMs de volume e/s elevada na ordem toostay dentro do limite de Olá de Olá volume de conta de armazenamento do Azure. Caso contrário, terá de toosee como pode equilibrar estas VMs entre contas de armazenamento diferentes sem atingir o limite de Olá de cada conta de armazenamento única. Obter mais detalhes são abordados na Olá [guia de implementação DBMS][dbms-guide]. Também devem ter estas limitações em mente para a aplicação de SAP pura server VMs ou outras VMs que exijam eventualmente VHDs adicionais.

Outro tópico que é relevante para as contas de armazenamento é se Olá VHDs numa conta de armazenamento está a obter georreplicação. A georreplicação está ativada ou desativada Olá nível de conta de armazenamento e não em Olá nível da VM. Se estiver ativada a georreplicação, Olá VHDs dentro Olá que conta de armazenamento seria replicada no outro Datacenter do Azure dentro Olá mesma região. Antes de decidir sobre isto, necessário pensar sobre Olá restrição os seguintes:

Replicação geográfica do Azure funciona localmente em cada VHD numa VM e não replicar o IOs Olá por ordem cronológica em vários VHDs numa VM. Por conseguinte, Olá VHD que representa Olá base VM, bem como quaisquer toohello de VHDs ligados VM adicional são replicadas independentes entre si. Isto significa que não há nenhuma sincronização entre Olá as alterações no Olá VHDs diferentes. Olá facto Olá IOs são replicadas independentemente da ordem de Olá em que são escritos significa que a georreplicação não é do valor para os servidores de base de dados que tenham as bases de dados distribuídas por vários VHDs. Na adição toohello DBMS, também poderão existir outras aplicações, onde os processos de escrita ou manipular dados VHDs diferentes e onde é importante tookeep ordem de Olá das alterações. Se for um requisito, não deve estar ativada georreplicação no Azure. Depende de se precisa ou pretender georreplicação para um conjunto de VMs, mas não para outro conjunto, pode já categorizar VMs e os seus VHDs relacionados para diferentes contas de armazenamento que têm a georreplicação ativada ou desativada.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Definição automount para discos ligados
- - -
> ![Windows][Logo_Windows] Windows
>
> Para VMs que são criadas a partir da própria imagens ou discos, é necessário toocheck e, possivelmente, defina o parâmetro de automount Olá. Definir este parâmetro permitirá Olá VM após um reinício ou a reimplementação no Azure toomount Olá anexado/montado unidades novamente automaticamente.
> parâmetro de Olá está definido para imagens de Olá fornecidas pela Microsoft no Olá Azure Marketplace.
>
> Na ordem tooset Olá automount, verifique a documentação de Olá de Olá linha de comandos executável diskpart.exe aqui:
>
> * [Opções da linha de comandos DiskPart](https://technet.microsoft.com/library/cc766465.aspx)
> * [Automount](http://technet.microsoft.com/library/cc753703.aspx)
>
> janela de linha de comandos do Windows Hello deve ser aberta como administrador.
>
> Se os discos estão anexados, terá de toolog para Olá de tooopen Olá VM Gestor de discos do Windows. Se não estiver ativada automount conforme recomendado nas capítulo [definição automount para discos ligados][planning-guide-5.5.3], Olá anexado recentemente volume > precisa de toobe colocado online e inicializar.
>
> ![Linux][Logo_Linux] Linux
>
> Tem tooinitialize um disco vazio anexado recentemente, conforme descrito no [neste artigo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Também precisa de tooadd novos discos toohello /etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Implementação final
Olá implementação final e os passos exatos, especialmente com que diz respeito toohello implementação de SAP expandido monitorização, consulte toohello [guia de implementação][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Aceder a sistemas SAP em execução em VMs do Azure
Para cenários apenas na nuvem, é aconselhável sistemas SAP tooconnect toothose em Olá internet pública através de SAP GUI. Para estes casos, Olá procedimentos seguintes têm de toobe aplicada.

Mais tarde no documento de Olá, vamos abordar Olá outros principais cenário, a ligação tooSAP sistemas nas implementações de vários locais que tenham uma ligação site a site (túnel VPN) ou a ligação de Azure ExpressRoute entre sistemas no local de Olá e do Azure.

### <a name="remote-access-toosap-systems"></a>Sistemas de tooSAP de acesso remotos
Com o Azure Resource Manager existem não existem pontos finais predefinidos já como modelo de clássico anteriores Olá. Todas as portas de uma VM de ARM do Azure estão abertas, desde que:

1. Nenhum grupo de segurança de rede está definido para a sub-rede de Olá ou interface de rede Olá. Tráfego de rede tooAzure VMs pode estar protegido por so-called "grupos de segurança de rede". Para obter mais informações consulte [o que é um grupo de segurança de rede (NSG)?][virtual-networks-nsg]
2. Nenhum Balanceador de carga do Azure está definido para a interface de rede Olá   

Consulte a diferença de arquitetura de Olá entre o modelo clássico e ARM conforme descrito em [neste artigo][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configuração de Olá SAP sistema e SAP GUI conectividade para o cenário de apenas na nuvem
Consulte este artigo que descreve o tópico de toothis detalhes: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Alterar as definições da Firewall dentro da VM
Poderá ser necessário tooconfigure firewall de Olá no seu tooallow de máquinas virtuais do tráfego tooyour SAP sistema de entrada.

- - -
> ![Windows][Logo_Windows] Windows
>
> Por predefinição, Olá dentro de uma VM do Azure implementada da Firewall do Windows está ativada. Tem agora tooallow Olá SAP porta toobe aberta, caso contrário Olá SAP GUI não será capaz de tooconnect.
> toodo isto:
>
> * Abra o painel de controlo e segurança \ Firewall definições de too'Advanced.
> * Agora, faça duplo clique em regras de entrada e escolha 'Nova regra'.
> * No Olá assistente seguinte escolheu toocreate uma nova regra de 'Porta'.
> * No Olá próximo passo do Assistente de Olá, deixe Olá TCP e tipo no número de porta de Olá que pretende tooopen. Uma vez que a nossa ID de instância do SAP 00, pegámos 3200. Se a instância tem um número de instância diferente, a porta de Olá definiu anteriormente com base no número de instância de Olá deve ser aberta.
> * Olá seguinte parte do Assistente de Olá, terá de item de Olá tooleave 'Ligação de permitir' marcada.
> * No passo seguinte do Olá do Assistente de Olá terá toodefine se regra Olá aplica-se à rede de domínio, privados e público. Ajuste-lo se precisar de tooyour necessário. No entanto, ligar-se com SAP GUI a partir de Olá fora através da rede pública Olá, terá de rede pública do toohave Olá regra aplicada toohello.
> * Olá último passo do Assistente de Olá, terá de toogive Olá um nome da regra e, em seguida, guardar a regra de Olá, premindo 'Terminar'
>
> regra de Olá entra em vigor imediatamente.
>
> ![Definição da regra de porta][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> imagens de Linux Olá na Olá Azure Marketplace não ative a firewall do iptables Olá por predefinição e sistema SAP Olá ligação tooyour deverão funcionar. Se estiver ativada iptables ou outra firewall,. consulte a documentação do toohello de iptables ou Olá utilizado firewall tooallow tráfego tcp de entrada demasiado 32xx de porta (onde xx é o número de sistema Olá do seu sistema SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Recomendações de segurança
Olá SAP GUI não ligar imediatamente tooany de instâncias SAP Olá (porta 32xx) que estão em execução, mas o primeiro liga através de Olá porta aberta toohello SAP mensagem processo do servidor (porta 36xx). Olá passado muito mesma porta do Olá foi utilizada pelo servidor de mensagem de Olá para instâncias da aplicação Olá comunicação interna toohello. tooprevent servidores no local aplicação inadvertidamente comunique com um servidor de mensagem no Azure Olá interno portas de comunicação podem ser alteradas. É altamente recomendável toochange Olá interno a comunicação entre Olá SAP servidor mensagens em fila e o número de porta diferente de tooa instâncias aplicação em sistemas que foi clonado a partir de sistemas no local, como um clone de desenvolvimento para fins de teste do projeto etc. Pode fazê-lo com o parâmetro de perfil predefinido Olá:

> rdisp/msserv_internal
>
>

conforme documentado no: <https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm>

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Conceitos de implementação apenas de nuvem de instâncias SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>VM única com SAP NetWeaver demonstração/formação cenário
![Com sistemas de demonstração de SAP VM únicos Olá mesmos nomes de VM, isolada na Cloud Services do Azure][planning-guide-figure-1700]

Neste cenário (consulte o capítulo [apenas na nuvem] [ planning-guide-2.1] deste documento) estiver a implementar um cenário de sistema típico formação/demonstração onde o cenário de formação completa/demonstração Olá está contido numa única VM. Iremos partem do princípio de que a implementação de Olá é feita através de modelos de imagem VM. Também partimos do pressuposto que múltiplo destas toobe de necessidade de VMs de demonstração/trainings implementado com Olá VMs ter Olá mesmo nome.

pressuposto Olá é que criou uma imagem de VM, conforme descrito em algumas secções de capítulo [preparar VMs com SAP para o Azure] [ planning-guide-5.2] neste documento.

sequência de Olá do cenário de Olá eventos tooimplement tem o seguinte aspeto:

[comment]: <> (Exemplo ARM tooprovide de ter MShermannd TODO / descrição utilizando o modelo json + esclarecimentos relativas à VM exclusivo dentro da rede virtual do ARM)   
##### <a name="powershell"></a>PowerShell
* Criar um novo grupo de resoure para cada horizontal de formação/demonstração

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```

* Criar uma nova conta de armazenamento

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Criar uma nova rede virtual para utilização de Olá cada formação/demonstração horizontal tooenable de Olá mesmo nome de anfitrião e endereços IP. rede virtual Olá está protegido por um grupo de segurança de rede que permita que apenas acesso de ambiente de trabalho remoto do tráfego tooport 3389 tooenable e a porta 22 para SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Criar um novo endereço IP público que pode ser utilizado tooaccess Olá excluir máquina virtual de Olá internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Criar uma nova interface de rede para a máquina virtual de Olá

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Crie uma máquina virtual. Para o cenário de apenas na nuvem Olá cada VM terão Olá mesmo nome. Olá SID de SAP da Olá NetWeaver SAP instâncias dessas VMs será Olá mesmo assim. Olá, no grupo de recursos do Azure, nome Olá Olá VM tem toobe exclusivo, mas em diferentes grupos de recursos do Azure pode executar as VMs com Olá mesmo nome. Olá, conta de 'Administrador' predefinida do Windows ou raiz para Linux não é válido. Por conseguinte, um novo nome de utilizador de administrador tem toobe definido, juntamente com uma palavra-passe. tamanho de Olá de Olá VM também tem de toobe definido.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES" -Skus "12" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="os"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"
$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Opcionalmente, adicione mais discos e restaurar o conteúdo necessário. Lembre-se de que todos os nomes de blob (URLs toohello blobs) tem de ser exclusivos no Azure.

```powershell
# Optional: Attach additional data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Olá, código de exemplo a seguir pode ser utilizado no Linux. Para Windows utilize PowerShell conforme descrito acima ou adaptar Olá exemplo toouse % rgName % em vez de $rgName e definir a variável de ambiente de Olá utilizando o comando de Windows hello *definir*.

* Criar um novo grupo de resoure para cada horizontal de formação/demonstração

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
azure group create $rgName "North Europe"
```

* Criar uma nova conta de armazenamento

```
azure storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku-name LRS $rgNameLower
```

* Criar uma nova rede virtual para utilização de Olá cada formação/demonstração horizontal tooenable de Olá mesmo nome de anfitrião e endereços IP. rede virtual Olá está protegido por um grupo de segurança de rede que permita que apenas acesso de ambiente de trabalho remoto do tráfego tooport 3389 tooenable e a porta 22 para SSH.

```
azure network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

azure network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
azure network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group-name SAPERPDemoNSG
```

* Criar um novo endereço IP público que pode ser utilizado tooaccess Olá excluir máquina virtual de Olá internet

```
azure network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --domain-name-label $rgNameLower --allocation-method Dynamic
```

* Criar uma nova interface de rede para a máquina virtual de Olá

```
azure network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-name SAPERPDemoPIP --subnet-name Subnet1 --subnet-vnet-name SAPERPDemoVNet
```

* Crie uma máquina virtual. Para o cenário de apenas na nuvem Olá cada VM terão Olá mesmo nome. Olá SID de SAP da Olá NetWeaver SAP instâncias dessas VMs será Olá mesmo assim. Olá, no grupo de recursos do Azure, nome Olá Olá VM tem toobe exclusivo, mas em diferentes grupos de recursos do Azure pode executar as VMs com Olá mesmo nome. Olá, conta de 'Administrador' predefinida do Windows ou raiz para Linux não é válido. Por conseguinte, um novo nome de utilizador de administrador tem toobe definido, juntamente com uma palavra-passe. tamanho de Olá de Olá VM também tem de toobe definido.

```
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn SUSE:SLES:12:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn RedHat:RHEL:7.2:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
#azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
```

* Opcionalmente, adicione mais discos e restaurar o conteúdo necessário. Lembre-se de que todos os nomes de blob (URLs toohello blobs) tem de ser exclusivos no Azure.

```
# Optional: Attach additional data disks
azure vm disk attach-new --resource-group $rgName --vm-name SAPERPDemo --size-in-gb 1023 --vhd-name datadisk
```

##### <a name="template"></a>Modelo
Pode utilizar modelos de exemplo de Olá no repositório de modelos do início rápido do azure Olá no github.

* [Simples VM com Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [VM do Windows simples](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [VM a partir da imagem](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementar um conjunto de VMs que precisam toocommunicate no Azure
Este cenário de apenas na nuvem é um cenário típico para fins de formação e demonstração onde hello software que representa Olá demonstração/formação cenário é distribuída por várias VMs. Olá diferentes componentes instalados no Olá diferentes VMs necessidade toocommunicate entre si. Novamente, neste cenário comunicação de rede não no local ou cenário entre locais é necessária.

Este cenário é uma extensão de instalação de Olá descrita capítulo [única VM com o SAP NetWeaver demonstração/formação cenário] [ planning-guide-7.1] deste documento. Neste caso mais máquinas virtuais, serão adicionadas tooan grupo de recursos existente. No Olá horizontal de formação de Olá de exemplo seguinte é composta por uma VM de ASCS/SCS SAP, uma VM com um DBMS e uma instância de servidor de aplicações SAP VM.

Antes de criar este cenário precisa toothink sobre as definições básicas como já executadas no cenário de Olá antes.

#### <a name="resource-group-and-virtual-machine-naming"></a>Grupo de recursos e a atribuição de nome de Máquina Virtual
Todos os nomes de grupo de recursos tem de ser exclusivos. Desenvolver o seu próprio esquema de nomenclatura dos seus recursos, tais como `<rg-name`>-sufixo.

nome da máquina virtual Olá tem toobe exclusivo dentro do grupo de recursos de Olá.

#### <a name="setup-network-for-communication-between-hello-different-vms"></a>A configuração rede para a comunicação entre Olá VMs diferentes
![Conjunto de VMs dentro de uma rede Virtual do Azure][planning-guide-figure-1900]

tooprevent nomenclatura colisões com clones de Olá mesmo landscapes de formação/demonstração, precisa de toocreate uma Azure Virtual Network para cada horizontal. Resolução de nomes DNS será fornecida pelo Azure ou pode configurar o próprio servidor DNS fora do Azure (não toobe mais abordado aqui). Neste cenário, não configure nosso própria DNS. Todas as máquinas virtuais dentro de uma rede Virtual do Azure será possível ativar a comunicação através de nomes de anfitrião.

Olá motivos pelos quais tooseparate landscapes de preparação ou de demonstração, redes virtuais e não apenas os recursos em grupos pode ser:

* Olá SAP landscape como conjunto de cópias de segurança tem da suas próprias OpenLDAP/AD e uma servidor de domínio necessidades toobe parte cada Olá landscapes.  
* Olá horizontal SAP como conjunto de cópias de segurança tem os componentes que toowork necessidade com endereços IP fixos.

Obter mais detalhes sobre redes virtuais do Azure e como toodefine-los podem ser encontrados na [neste artigo][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Implementar o SAP VMs com conectividade de rede empresarial (em vários locais)
Executar uma horizontal SAP e quiser toodivide Olá implementação entre bare-metal para servidores DBMS gama alta de classe, ambientes no local virtualizado para as camadas da aplicação e mais pequenos de camada de 2 configurado IaaS do Azure e sistemas SAP. pressuposto base Olá é que os sistemas SAP dentro de um horizontal SAP têm toocommunicate entre si e com muitos outros componentes de software implementadas na empresa Olá, independentemente da respetiva formulário de implementação. Também não deverá haver nenhum diferenças introduzidas pelo formulário de implementação de Olá para utilizador final de Olá ligar com SAP GUI ou outras interfaces. Estas condições só podem ser preenchidas quando criarmos Olá no local Active Directory/OpenLDAP e os serviços DNS expandido toohello sistemas do Azure através da conectividade de site-a-site/várias-site ou ligações privadas, como o Azure ExpressRoute.

Na ordem tooget mais em segundo plano nos detalhes de implementação de Olá do SAP no Azure, Aconselhamo-lo tooread capítulo [implementação conceitos de Cloud-Only de instâncias SAP] [ planning-guide-7] deste documento para o qual explica algumas noções básicas de Olá construções do Azure e como estes devem ser utilizadas com aplicações SAP no Azure.

### <a name="scenario-of-a-sap-landscape"></a>Cenário de numa horizontal SAP
cenário de vários locais Olá pode ser aproximadamente descrito como em gráficos de Olá abaixo:

![Conetividade site a Site no local e de recursos do Azure][planning-guide-figure-2100]

Olá cenário mostrado acima descreve um cenário onde Olá no local AD/OpenLDAP e o DNS está expandido tooAzure. No lado do Olá no local, um determinado intervalo de endereços IP é reservado por subscrição do Azure. intervalo de endereços IP Olá será atribuído tooan Azure Virtual Network na Olá do lado do Azure.

#### <a name="security-considerations"></a>Considerações de segurança
Olá requisito mínimo é Olá utilização dos protocolos de comunicação segura, tais como o SSL/TLS para acesso ao browser ou ligações baseados na VPN para o sistema aceder toohello Azure serviços. pressuposto Olá é que as empresas processam de forma muito diferente ligação de VPN Olá entre a sua rede empresarial e o Azure. Algumas empresas blankly poderão abrir todas as portas de Olá. Algumas outras empresas querer toobe muito precisas nas portas que precisam tooopen, etc.

Na tabela de Olá abaixo SAP típico portas de comunicação estão listadas. Basicamente é suficiente tooopen Olá porta de gateway SAP.

| Serviço | Nome de porta | Exemplo `<nn`> = 01 | Intervalo predefinido (min máx.) | Comentário |
| --- | --- | --- | --- | --- |
| Distribuidor |sapdp`<nn>` consulte * |3201 |3200 – 3299 |Distribuidor SAP, utilizado por SAP GUI para Windows e o Java |
| Servidor de mensagens |sapms`<sid`> consulte * * |3600 |sapms livre`<anySID`> |SID = o ID de sistema de SAP |
| Gateway |sapgw`<nn`> consulte * |3301 |Livre |Gateway SAP, utilizada para comunicação CPIC e RFC |
| Router SAP |sapdp99 |3299 |Livre |Os nomes de serviço de CI (instância central) apenas podem ser reatribuídos /etc/services tooan arbitrários valor após a instalação. |

*) nn = número da instância do SAP

*) sid = o ID de sistema de SAP

Informações mais detalhadas sobre as portas necessárias para diferentes produtos SAP ou serviços por produtos SAP podem ser encontrados aqui <http://scn.sap.com/docs/DOC-17124>.
Com este documento deve ser capaz de tooopen dedicado portas no dispositivo VPN de Olá necessário para cenários e produtos SAP específicos.

Outra segurança mede quando implementar VMs neste cenário, poderá ser toocreate um [grupo de segurança de rede] [ virtual-networks-nsg] toodefine regras de acesso.

### <a name="dealing-with-different-virtual-machine-series"></a>Lidar com a série de Máquina Virtual diferente
No decorrer de Olá dos últimos 12 meses Microsoft adicionados muitos tipos VM mais diferem no número de vCPUs, memória ou mais importantes no hardware que é executada. Nem todos os dessas VMs são suportadas com SAP (consulte suportado tipos VM na nota SAP [1928533]). Algumas dessas VMS executam gerações de hardware de outro anfitrião. Estes gerações de hardware do anfitrião são obter implementadas na granularidade Olá de uma Azure-unidade de escala. Casos de significa que podem surgir onde Olá diferentes tamanhos de VM, escolha não pode ser executada no Olá mesma de unidade de escala. Um conjunto de disponibilidade é limitado em Olá capacidade toospan unidades de escala com base em hardware diferente.  Por exemplo, Se quiser toorun Olá DBMS em VMs A5 A11 e Olá camada de aplicação de SAP em VMs de série de G, seria possível toodeploy forçada um único SAP ou sistemas SAP diferentes dentro de diferentes conjuntos de disponibilidade.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Imprimir a uma impressora de rede local da instância do SAP no Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Impressão através de TCP/IP no cenário entre locais
Configurar as impressoras de rede de TCP/IP com base no local na VM do Azure é global Olá, mesmo que a sua rede empresarial, partindo do princípio de dispõe de um túnel VPN Site a Site ou a ligação do ExpressRoute estabelecida.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo isto:
>
> * Algumas impressoras de rede são fornecidos com um Assistente de configuração que torna mais fácil tooset cópias de segurança a impressora na VM do Azure. Se nenhum software de assistente tiver sido distribuído com a forma "manual" de impressora Olá tooset segurança impressora Olá é toocreate uma nova porta de impressora TCP/IP.
> * Abra o painel de controlo -> dispositivos e impressoras -> Adicionar uma impressora
> * Selecione adicionar uma impressora utilizando um endereço de TCP/IP ou nome de anfitrião
> * Escreva Olá endereço IP da impressora Olá
> * Porta de impressora 9100 padrão
> * Se for necessário instale manualmente o controlador de impressora adequadas Olá.
>
> ![Linux][Logo_Linux] Linux
>
> * como do Windows apenas siga Olá procedimento padrão tooinstall uma impressora de rede
> * Basta seguir públicos Linux guias Olá para [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) ou [Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) sobre tooadd uma impressora.
>
>

- - -
![Impressão de rede][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Impressora baseada no anfitrião através de SMB (impressora partilhada) no cenário entre locais
Impressoras baseada no anfitrião não são compatíveis rede por predefinição. Mas uma impressora baseada no anfitrião pode ser partilhada entre os computadores numa rede, desde que impressoras Olá é ligado tooa ligado no computador. Ligar a sua empresa de rede ou o Site para Site como o ExpressRoute e partilhar a impressora local. Olá protocolo SMB utiliza NetBIOS em vez de DNS como serviço de nomes. nome de anfitrião NetBIOS Olá pode ser diferente do nome de anfitrião DNS Olá. caso padrão Olá é que o nome de anfitrião NetBIOS Olá e o nome de anfitrião DNS Olá são idênticos. domínio DNS Olá não fazer sentido no espaço de nomes de NetBIOS Olá. Olá em conformidade, o nome de anfitrião DNS completamente qualificado, constituída por nome de anfitrião DNS Olá e o domínio DNS não podem ser utilizado no espaço de nomes de NetBIOS Olá.

partilha de impressoras Olá é identificada por um nome exclusivo numa rede de Olá:

* Nome de anfitrião do anfitrião SMB Olá (sempre necessário).
* Nome da partilha de Olá (sempre necessário).
* Nome do domínio Olá se a partilha de impressoras não está a ser Olá mesmo domínio que o sistema SAP.
* Além disso, um nome de utilizador e uma palavra-passe podem ser necessários tooaccess Olá impressora partilha.

Como:

- - -
> ![Windows][Logo_Windows] Windows
>
> Partilhe a impressora local.
> Olá VM do Azure abra Olá Explorador do Windows e escreva o nome da partilha Olá impressora Olá.
> Um Assistente de instalação da impressora irá ajudá-lo durante o processo de instalação de Olá.
>
> ![Linux][Logo_Linux] Linux
>
> Seguem-se alguns exemplos de documentação sobre configurar impressoras de rede no Linux ou, incluindo um capítulo relativos à impressão no Linux. Irá funcionar Olá mesma maneira no VM Linux do Azure, desde Olá VM faz parte de uma VPN:
>
> * SLES <_Share_or_Windows_Share https://en.opensuse.org/SDB:Printing_via_SMB_ (Samba)>
> * RHEL <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-printing-smb-printer.html>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Impressora de USB (reencaminhamento impressoras)
Capacidade de Olá do Azure de acesso de Olá Olá dos serviços de ambiente de trabalho remoto tooprovide utilizadores tootheir dispositivos de impressora local numa sessão remota não está disponível.

- - -
> ![Windows][Logo_Windows] Windows
>
> Obter mais detalhes sobre impressão com o Windows podem ser encontrados aqui: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integração do SAP sistemas do Azure para a correção e o sistema de transporte (TMS) em vários locais
Olá tooexport de toobe configurado tem de alterar o SAP e sistema de transporte (TMS) e importe o pedido de transporte entre sistemas operativos na horizontal Olá. Iremos partem do princípio de que as instâncias de desenvolvimento de Olá de um sistema SAP (desenvolvimento) estão localizadas no Azure, enquanto a garantia de qualidade de Olá (pergunta e resposta) e sistemas produtivos (PRD) estão no local. Além disso, partimos do princípio que há um diretório de transporte central.

##### <a name="configuring-hello-transport-domain"></a>Configurar Olá domínio de transporte
Configurar o seu domínio de transporte no sistema de Olá designado como Olá controlador de domínio de transporte, conforme descrito em [Olá de configurar o controlador de domínio de transporte](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Um utilizador do sistema que TMSADM será criada Olá necessários e o destino de RFC será gerado. Pode verificar estas ligações de RFC utilizando a transação de Olá SM59. Resolução de nome de anfitrião deve ser ativada através do seu domínio de transporte.

Como:

* No nosso cenário decidimos Olá no local sistema QAS será o controlador de domínio de CTS Olá. Chame transação STMS. é apresentada a caixa de diálogo TMS Olá. É apresentada uma caixa de diálogo de configurar o domínio de transporte. (Esta caixa de diálogo só é apresentada se ainda não tiver configurado a um domínio de transporte.)
* Certifique-se de que o utilizador Olá criado automaticamente está autorizado TMSADM (SM59 -> ABAP ligação -> TMSADM@E61.DOMAIN_E61 -> detalhes -> Utilities(M) -> autorização teste). ecrã inicial do Olá da transação STMS deve mostrar que este sistema de SAP está agora a funcionar como controlador de Olá do domínio de transporte de Olá conforme mostrado aqui:

![Ecrã inicial de transação STMS no controlador de domínio Olá][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Incluindo sistemas SAP no Olá domínio de transporte
sequência de Olá, incluindo um sistema SAP num domínio transporte procura da seguinte forma:

* No Olá DEV sistema no Azure aceda toohello sistema de transporte (cliente 000) e chamada de transação STMS. Escolha outra configuração a partir da caixa de diálogo Olá e continuar com o sistema incluem no domínio. Especificar Olá controlador de domínio como o anfitrião de destino ([, incluindo sistemas de SAP no domínio de transporte de Olá](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). sistema de Olá está agora toobe espera incluído no domínio de transporte de Olá.
* Por motivos de segurança, em seguida, tiver tooconfirm de controlador de domínio de back-toohello toogo o pedido. Escolha a descrição geral do sistema e aprovar do sistema de espera de Olá. Em seguida, confirme a configuração de linha de comandos e Olá Olá será distribuída.

Este sistema SAP contém as informações necessárias Olá sobre Olá todos os outros sistemas SAP no domínio de transporte de Olá. Em Olá mesmo tempo, endereço Olá envio de dados do sistema SAP novo Olá tooall Olá outros sistemas SAP e Olá sistema SAP é introduzido no perfil de transporte de Olá do programa de controlo de transporte de Olá. Verifique se RFCs e acesso ao diretório de transporte de toohello do domínio Olá de trabalho.

Continuar com a configuração de Olá do seu sistema de transporte como habitualmente, tal como descrito na documentação de Olá [alteração e do sistema de transporte](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Como:

* Certifique-se a que sua STMS no local está configurado corretamente.
* Certifique-se de que o nome de anfitrião de Olá do controlador de domínio de transporte de Olá pode ser resolvido pela máquina virtual no Azure e vice-versa visa.
* Chamada de transação STMS -> configuração outros incluem-> sistema-no domínio.
* Certifique-se a ligação de Olá no Olá no sistema TMS local.
* Configure camadas, grupos e rotas de transporte como habitualmente.

No site para site ligados cenários de vários locais, latência de Olá entre no local e o Azure ainda pode ser significativo. Se iremos seguir Olá sequência de transporte objetos através de desenvolvimento e teste tooproduction de sistemas ou pensar aplicar transportes ou toohello diferentes sistemas de pacotes de suporte, tenha em atenção que, dependente na localização de Olá transporte central Olá diretório, alguns dos sistemas de Olá irão encontrar latência elevada ler ou escrever dados no diretório de transporte central Olá. situação Olá é configurações de horizontal tooSAP semelhantes em que sistemas diferentes de Olá são distribuídos através de centros de dados diferentes com substancial distância entre centros de dados de Olá.

Na ordem toowork em torno essa latência e têm sistemas Olá funcionam rápida no ler ou escrever tooor do diretório de transporte de Olá, pode configurar dois domínios de transporte STMS (uma para no local. e outra com os sistemas de Olá em domínios de transporte de Olá do Azure e a ligação Verifique esta documentação para o qual explica Olá princípios envolvidos neste conceito no Olá SAP TMS: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Como:

* Configurar um domínio de transporte em cada localização (no local e do Azure) utilizando a transação STMS <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Associar a domínios Olá com uma ligação de domínio e confirmar Olá ligação entre dois domínios de Olá.
  <http://help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Distribua o sistema de configuração de Olá toohello ligado.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Tráfego RFC entre instâncias SAP localizado no Azure e no local (em vários locais)
Toowork de necessidades de tráfego RFC entre os sistemas que estão no local e no Azure. toosetup uma ligação chamada transação SM59 num sistema de origem em que seja necessário toodefine uma ligação de RFC para sistema de destino Olá. a configuração de Olá é semelhante toohello de configuração padrão de uma ligação de RFC.

Partimos do princípio que, no cenário de vários locais Olá, VMs Olá que executam sistemas SAP que necessitam de toocommunicate entre si estão em Olá mesmo domínio. Por conseguinte hello a configuração de uma ligação de RFC entre sistemas SAP não diferem do passos de configuração de Olá e entradas em cenários no local.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Ao aceder aos fileshares 'local' de instâncias SAP localizadas no Azure ou vice versa
Instâncias SAP localizadas no Azure necessário tooaccess partilhas de ficheiros que estão dentro do local de empresa Olá. Além disso, as instâncias SAP no local têm tooaccess partilhas de ficheiros que estão localizadas no Azure. tooenable Olá as partilhas de ficheiros tem de configurar permissões de Olá e opções de partilha no sistema local Olá. Certifique-se de que tooopen Olá de portas Olá VPN ou ligação do ExpressRoute entre o Azure e o seu centro de dados.

## <a name="supportability"></a>Suportabilidade
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Azure solução de monitorização para SAP
Na ordem tooenable Olá monitorização dos sistemas SAP crítico de missão no Azure Olá SAP ferramentas de monitorização SAPOSCOL ou o agente do anfitrião SAP obter dados do anfitrião do serviço de Máquina Virtual do Azure Olá através de uma extensão de monitorização do Azure para SAP. Uma vez que Olá exigências por SAP foram aplicações tooSAP muito específico, Microsoft decidiu não toogenerically implementar Olá necessária a funcionalidade no Azure, mas deixe-a para clientes toodeploy Olá necessário monitorização componentes e as configurações tootheir Máquinas virtuais em execução no Azure. No entanto, o ciclo de vida de implementação e gestão de componentes de monitorização de Olá irá ser principalmente automatizada pelo Azure.

#### <a name="solution-design"></a>Design de solução
solução Olá desenvolvidas tooenable que SAP monitorização baseia-se na arquitetura de Olá do agente da VM do Azure e a arquitetura de extensão. ideia Olá do framework de agente da VM do Azure e a extensão de Olá é tooallow instalação de aplicações de software disponíveis na Galeria de extensão da VM do Azure Olá dentro de uma VM. Olá princípio ideia atrás este conceito é tooallow (em casos como Olá extensão de monitorização do Azure para SAP), Olá a implementação da funcionalidade especial para uma configuração de VM e Olá desse software no momento da implementação.

Desde Fevereiro de 2014, hello 'Agente da VM do Azure' que ativa o processamento de extensões de VM do Azure específicas dentro Olá que VM é injetada VMs do Windows por predefinição na criação de VM no Olá Portal do Azure. Em caso de Olá SUSE ou Red Hat Linux agente da VM já faz parte da imagem do Azure Marketplace. No caso de um seria carregar uma VM com Linux a partir do agente da VM no local tooAzure Olá tem toobe instalado manualmente.

Olá blocos modulares básicos da solução de monitorização de Olá no Azure para SAP tem o seguinte aspeto:

![Componentes de extensão do Microsoft Azure][planning-guide-figure-2400]

Como é mostrado no diagrama de blocos de Olá acima, uma parte da solução de monitorização para SAP de Olá está alojada no Olá imagem de VM do Azure e Galeria de extensão do Azure que é um repositório replicado globalmente, que é gerido por operações do Azure. É Olá responsabilidade da equipa SAP/MS conjunta Olá Olá implementação do Azure do SAP toowork com novas versões de operações do Azure toopublish de Olá extensão de monitorização do Azure para SAP a trabalhar. Esta extensão de monitorização do Azure para SAP utilizará Olá Linux do Azure Diagnostics (LAD) ou extensão de diagnóstico de Azure da Microsoft (WAD) tooget Olá informações necessárias.

Ao implementar uma nova VM do Windows, é adicionado automaticamente Olá 'Agente da VM do Azure' para Olá VM. função de Olá deste agente é Olá toocoordinate carregar e a configuração de Olá extensões do Azure para a monitorização do SAP NetWeaver sistemas. Para VMs com Linux Olá agente da VM do Azure já faz parte Olá Azure Marketplace da imagem do SO.

No entanto, é um passo que continua a necessitar de toobe executada pelo cliente de Olá. Esta é a ativação de Olá e a configuração de recolha de desempenho de Olá. Olá relacionados com o processo toohello 'Configuração' é um processo automatizada por um script do PowerShell ou comando da CLI. pode ser transferido Olá script do PowerShell Olá Microsoft Azure Script Center, conforme descrito em Olá [guia de implementação][deployment-guide].

Olá arquitetura geral de Olá Azure solução de monitorização para SAP aspeto:

![Solução de monitorização para SAP NetWeaver do Azure][planning-guide-figure-2500]

**Para Olá exato como-tooand para obter passos detalhados de utilizar estes cmdlets do PowerShell ou comando da CLI durante as implementações, siga as instruções de Olá indicadas na Olá [guia de implementação][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integração do Azure localizado instância do SAP para SAProuter
Instâncias SAP em execução no Azure necessário toobe acessível a partir do SAProuter bem.

![Ligação de rede de SAP Router][planning-guide-figure-2600]

Um SAProuter permite a comunicação de TCP/IP Olá entre sistemas participantes se não houver nenhuma ligação direta do IP. Esta opção fornece partido Olá que não é necessária nenhuma ligação de ponto a ponto entre parceiros de comunicação de Olá no nível de rede. Olá SAProuter está a escutar na porta 3299 por predefinição.
instâncias de tooconnect SAP através de um SAProuter terá toogive Olá SAProuter cadeia e o nome de anfitrião com tooconnect qualquer tentativa.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Até ao momento Olá foco Olá documento foi SAP NetWeaver em geral, ou Olá pilha do SAP NetWeaver ABAP. Nesta secção pequeno, considerações específicas de pilha de SAP Java Olá estão listadas. Uma das Olá SAP NetWeaver Java exclusivamente baseado em aplicações mais importante é Olá SAP Enterprise Portal. Outros SAP NetWeaver com base em aplicações como o SAP instalador de plataforma e o Gestor de solução do SAP utilizam Olá SAP NetWeaver ABAP e pilhas de Java. Por conseguinte, certamente há uma necessidade tooconsider aspetos específicos relacionados toohello SAP NetWeaver Java pilha bem.

### <a name="sap-enterprise-portal"></a>Portal da empresa SAP
a configuração de um Portal de SAP uma Máquina Virtual no Azure Olá não diferem dos de uma instalação local no se estiver a implementar em cenários de vários locais. Desde Olá que DNS é feito no local, definições de porta de Olá de instâncias individuais Olá podem ser feitas como configurado no local. recomendações de Olá e restrições descritas neste documento, até ao momento aplicam-se para uma aplicação, como o SAP Enterprise Portal ou a pilha de SAP NetWeaver Java Olá em geral.

![Portal de expostas SAP][planning-guide-figure-2700]

Um cenário de implementação especiais por alguns clientes é a exposição de direta Olá de Olá SAP Enterprise Portal toohello Internet enquanto o anfitrião da máquina virtual Olá está ligado toohello rede da empresa através do túnel VPN de site para site ou ExpressRoute. Para um cenário, tem de certificar de que as portas específicas são abertos e não bloqueadas por grupo de segurança de rede ou firewall toomake. Olá mechanics mesmo teria toobe aplicada quando pretender que a instância de SAP Java tooan tooconnect no local num cenário apenas na nuvem.

portal de inicial Olá URI é http (s):`<Portalserver`>: 5XX00/irj onde tem o formato da porta de Olá por 50000 mais (Systemnumber × 100). Olá predefinido portal URI de SAP sistema 00 é `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Para obter mais detalhes, tem um aspeto um <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Configuração de ponto final][planning-guide-figure-2800]

Se pretender que o URL de Olá toocustomize e/ou as portas do Portal da empresa do SAP, verifique esta documentação:

* [Alterar o URL do Portal](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Alterar os números de porta predefinidos, números de porta do Portal](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

<a name="7cf991a1-badd-40a9-944e-7baae842a058"></a>
## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Elevada disponibilidade (ed) e recuperação de desastre (DR) para NetWeaver SAP em execução em Azure Virtual Machines
### <a name="definition-of-terminologies"></a>Definição de terminologies
Olá termo **elevada disponibilidade (HA)** é tooa relacionada, geralmente, conjunto de tecnologias que minimiza interrupções de IT, fornecendo a continuidade do negócio de serviços de TI através de redundante, com tolerância a falhas ou componentes de protegido de ativação pós-falha dentro de Olá **mesmo** Centro de dados. No nosso caso, dentro de uma região do Azure.

**Recuperação após desastre (DR)** está também direcionado para minimizar perturbações de serviços IT e os respetivos recuperação mas across **diferentes** centros de dados, que são normalmente localizada centenas de kilometers ausente. No nosso caso, normalmente, entre diferentes regiões Azure Olá mesma região geopolítica ou conforme estabelecido por si, como um cliente.

### <a name="overview-of-high-availability"></a>Descrição geral da elevada disponibilidade
Iremos pode separar debate Olá sobre SAP elevada disponibilidade no Azure em duas partes:

* **Elevada disponibilidade da infraestrutura do Azure**, por exemplo, HA de (VMs) de computação, rede, armazenamento, etc. e suas vantagens para aumentar a disponibilidade de aplicações SAP.
* **Disponibilidade elevada da aplicação do SAP**, por exemplo, os componentes de software do HA do SAP:
  * Servidores de aplicações SAP
  * Instância do SAP ASCS/SCS
  * Servidor de base de dados

e como pode ser combinado com a infraestrutura do Azure HA.

SAP elevada disponibilidade no Azure tem algumas tooSAP diferenças em comparação com elevada disponibilidade num ambiente físico ou virtual no local. Olá documento seguinte do SAP descreve padrão configurações de SAP elevada disponibilidade em ambientes virtualizados no Windows: <http://scn.sap.com/docs/DOC-44415>. Não está integrado em sapinst SAP-HA uma configuração para Linux, tal como existe para o Windows. Relativamente à HA do SAP no local para Linux encontrar mais informações aqui: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Elevada disponibilidade da infraestrutura do Azure
Não há nenhum SLA de VM única disponíveis em Azure Virtual Machines neste momento. tooget uma ideia como disponibilidade Olá de uma única VM poderá ter o aspeto como pode simplesmente criar produto Olá Olá diferentes SLA do Azure disponíveis: <https://azure.microsoft.com/support/legal/sla/>.

base de Olá para um cálculo Olá é 30 dias, por mês ou 43200 minutos. Por conseguinte, o período de indisponibilidade 0,05% corresponde too21.6 minutos. Normalmente, disponibilidade Olá dos serviços diferentes Olá será multiplicar no Olá seguinte forma:

(Serviço de disponibilidade #1/100) * (serviço de disponibilidade #2/100) * (serviço de disponibilidade #3/100) *...

Como:

(99,95/100) * (99,9/100) * (99,9/100) = 0.9975 ou um disponibilidade global da 99.75%.

#### <a name="virtual-machine-vm-high-availability"></a>Elevada disponibilidade de máquina virtual (VM)
Existem dois tipos de eventos de plataforma Azure que podem afetar a disponibilidade de Olá das suas máquinas virtuais: a ser planeada a manutenção e a manutenção não planeada.

* Manutenção planeada eventos são atualizações periódicas efetuadas pelo toohello Microsoft subjacente tooimprove da plataforma Azure fiabilidade geral, o desempenho e segurança da infraestrutura de plataforma de Olá executar as máquinas virtuais.
* Eventos de manutenção não planeada ocorrerem quando a infraestrutura física subjacente a máquina virtual ou de hardware de Olá Ocorreu uma falha de alguma forma. Isto pode incluir falhas de rede local, falhas de disco local ou outras falhas estruturais. Quando é detetada uma falha de tal, o Olá plataforma do Azure irá migrar automaticamente a máquina virtual de Olá de servidor físico mau estado de funcionamento que aloja o servidor de físico bom estado de funcionamento com tooa de máquina virtual. Esses eventos são raros, mas também podem fazer com que o tooreboot de máquina virtual.

Podem encontrar mais detalhes nesta documentação: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Redundância do armazenamento do Azure
dados de Olá na sua conta de armazenamento do Microsoft Azure estão sempre replicados tooensure durabilidade e elevada disponibilidade, que responde Olá SLA de armazenamento do Azure, mesmo em enfrentam Olá de falhas de hardware transitórias

Uma vez que o armazenamento do Azure consiste em manter 3 imagens dos dados de Olá por predefinição, RAID5 ou RAID1 entre múltiplos discos do Azure não são necessários.

Podem encontrar mais detalhes neste artigo: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>A utilização de reinício de VM de infraestrutura do Azure tooAchieve "Availability superior" das aplicações SAP
Se decidir não toouse funcionalidades como o servidor de ativação pós-falha Clustering Windows (WSFC) ou um Linux equivalente (Olá última um ainda não é suportado no Azure em combinação com o software SAP), o reinício de VM do Azure é tooprotect sobreutilizado um sistema de SAP contra planeada e período de indisponibilidade não planeado de infraestrutura de servidor físico do Azure Olá e global plataforma Azure subjacente.

> [!NOTE]
> É importante toomention que principalmente reiniciar de VM do Azure protege VMs e não aplicações. Reinício de VM não oferece elevada disponibilidade para aplicações SAP, mas oferecem um determinado nível de disponibilidade da infraestrutura e, por isso indiretamente "maior disponibilidade" dos sistemas SAP. Não há também nenhum SLA durante o período de tempo de Olá demorará toorestart uma VM após uma falha de anfitrião planeadas ou imprevistas. Por conseguinte, este método de 'elevada disponibilidade' não é adequado para componentes mais importantes de um sistema SAP como (A) SCS ou DBMS.
>
>

Outro elemento importante da infraestrutura de elevada disponibilidade é armazenamento. Por exemplo, SLA de armazenamento do Azure é uma disponibilidade mínima de 99,9%. Se um implementa todas as VMs com os respetivos discos para uma conta do Storage do Azure único, potenciais indisponibilidade fará com que a indisponibilidade de todas as VMs que são colocadas nessa conta do Storage do Azure e também todos os SAP componentes que estejam dessas VMs em execução do armazenamento do Azure.  

Em vez de colocando todas as VMs para uma única conta de armazenamento do Azure, também pode utilizar o armazenamento dedicado contas para cada VM e, desta forma aumentam a disponibilidade geral de VM e SAP da aplicação através da utilização de várias contas do Storage do Azure independentes.

Um exemplo de arquitetura de um sistema de SAP NetWeaver que utiliza a infraestrutura do Azure HA pode ter o seguinte aspeto:

![Utilizar a infraestrutura do Azure HA tooachieve SAP "superior" de disponibilidade de aplicações][planning-guide-figure-2900]

Para componentes mais importantes do SAP foi alcançada Olá seguir até ao momento:

* Elevada disponibilidade dos servidores de aplicações SAP (AS)

Instâncias de servidor de aplicações SAP são os componentes redundantes. Cada SAP como instância está implementada na sua própria VM, que está a ser executado noutra falhas do Azure e o domínio de atualização (consulte capítulos [domínios de falhas] [ planning-guide-3.2.1] e [atualizar domínios][planning-guide-3.2.2]). Isto é certificar-se ao utilizar conjuntos de disponibilidade do Azure (consulte o capítulo [conjuntos de disponibilidade do Azure][planning-guide-3.2.3]). Potencial indisponibilidade planeada ou não planeada de um índice de falhas do Azure ou o domínio de atualização irá fazer com que indisponibilidade de um número restrito de VMs com as respetivas SAP AS instâncias.
Cada SAP como instância é colocada na sua própria conta do Storage do Azure – potencial indisponibilidade de uma conta de armazenamento do Azure irá fazer com que indisponibilidade de apenas uma VM com AS respetivas SAP instância. No entanto, tenha em atenção de que há um limite de contas do Storage do Azure dentro de uma subscrição do Azure. tooensure início automático (A) instância SCS depois de reiniciar o computador Olá VM, certifique-se tooset Autostart parâmetro na instância (A) SCS iniciar perfil descrito capítulo [utilizando Autostart para instâncias SAP][planning-guide-11.5].
Leia também capítulo [elevada disponibilidade para servidores de aplicações SAP] [ planning-guide-11.4.1] para obter mais detalhes.

* *Superior* instância SCS de disponibilidade do SAP (A)

Aqui vamos utilizar reiniciar de VM do Azure tooprotect Olá VM com instâncias de SCS SAP (A) instalada. No hello maiúsculas e minúsculas de um período de indisponibilidade planeado ou não planeada do Azure servidores, as VMs que irão ser reiniciadas noutro servidor disponível. Conforme mencionado anteriormente, principalmente reiniciar de VM do Azure protege VMs e não aplicações, neste caso, hello (A) instância SCS. Através de Olá reiniciar a VM que irá aceder indiretamente "availability superior" da instância do SCS SAP (A). tooinsure início automático (A) instância SCS depois de reiniciar o computador Olá VM, certifique-se tooset Autostart parâmetro na instância (A) SCS iniciar perfil descrito capítulo [utilizando Autostart para instâncias SAP][planning-guide-11.5]. Isto significa que a instância do SCS Olá (A) como um ponto único de falha (SPOF) em execução numa única VM será fator de determinative Olá para disponibilidade Olá horizontal SAP todo Olá.

* *Superior* disponibilidade de servidor DBMS

Aqui, instância de SAP (A) SCS toohello semelhante utilizar as maiúsculas e minúsculas, iremos utilizar o reinício de VM do Azure tooprotect Olá VM com o software instalado DBMS e iremos alcançar a "elevada disponibilidade" software DBMS através de reiniciar a VM.
DBMS em execução numa VM única também é um SPOF e é fator de determinative Olá para disponibilidade Olá horizontal SAP todo Olá.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Aplicação de SAP elevada disponibilidade no IaaS do Azure
tooachieve completa SAP elevada disponibilidade do sistema, é necessário tooprotect todas as críticos SAP componentes do sistema, por exemplo, redundantes servidores de aplicações SAP, e componentes exclusivos (por exemplo, único ponto da falha) como instância SCS SAP (A) e o DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Elevada disponibilidade para servidores de aplicações SAP
Para instâncias de caixa de diálogo/servidores de aplicações de SAP Olá não é necessário toothink sobre uma solução de elevada disponibilidade específico. Elevada disponibilidade simplesmente é conseguida através da redundância e assim ter espaço suficiente-las nos diferentes máquinas virtuais. Eles devem todos os colocadas num Olá tooavoid mesmo conjunto de disponibilidade do Azure que Olá VMs pode ser atualizado em Olá simultâneo durante o período de indisponibilidade de manutenção planeada. a funcionalidade básico Olá que baseia-se em diferentes domínios de falhas dentro de uma unidade de escala do Azure e a atualização já foi introduzida no capítulo [atualizar domínios][planning-guide-3.2.2]. Conjuntos de disponibilidade do Azure eram apresentados no capítulo [conjuntos de disponibilidade do Azure] [ planning-guide-3.2.3] deste documento.

Não há nenhum infinito número de falhas e domínios de atualização de mensagens em fila que podem ser utilizados por um conjunto de disponibilidade do Azure dentro de uma unidade de escala do Azure. Isto significa que colocar um número de VMs para um conjunto de disponibilidade mais cedo ou posterior no facto de Olá mais do que uma VM termina no Olá falhas mesma ou domínio de atualização

Implementar o servidor de aplicações SAP algumas instâncias no respetivos VMs dedicadas e partindo do princípio que obtivemos 5 domínios de atualização, Olá seguinte imagem emerges no fim de Olá. número máximo real Olá de domínios de falhas e atualização dentro de um conjunto de disponibilidade poderá alterar no Olá futura:

![HA dos servidores de aplicações SAP no Azure][planning-guide-figure-3000]

Podem encontrar mais detalhes nesta documentação: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Elevada disponibilidade para a instância de SAP (A) SCS Olá no Windows
Cluster de ativação pós-falha de servidor do Windows (WSFC) é uma instância SCS SAP (A) de Olá de tooprotect de soluções utilizadas frequentemente. Também está integrado em sapinst na forma de uma instalação"HA". Neste ponto no tempo Olá infraestrutura do Azure não é possível tooprovide Olá funcionalidade tooset segurança Olá de Cluster de ativação pós-falha do Windows Server Olá necessário mesmo a forma como é efetuada no local.

A partir de Janeiro de 2016 plataforma de nuvem do Azure Olá com sistema de operativo do Windows hello não fornece a possibilidade de Olá de utilizar um volume partilhado de cluster num disco partilhado entre duas VMs do Azure.

Uma solução válida é apesar utilização Olá do software de terceiros 3rd que fornece um volume partilhado através da replicação de disco síncrona e transparente, que pode ser integrada no WSFC. Esta abordagem implica que esse nó de cluster ativo Olá só é possível tooaccess um dos discos de Olá copia um ponto no tempo. A partir de Janeiro de 2016 este HA configuração é suportada tooprotect Olá corresponde uma instância SCS SAP (A) no Windows SO convidado em VMs do Azure em combinação com o software de terceiros 3rd SIOS DataKeeper.

Olá SIOS DataKeeper solução fornece um tooWindows de recurso de cluster de disco partilhado Clusters de ativação pós-falha, fazendo com que:

* Um VHD de Azure adicionais ligado tooeach de Olá as máquinas virtuais (VMs) que estão numa configuração de Cluster do Windows
* SIOS DataKeeper Cluster Edition em execução em ambos os nós VM
* Ter SIOS DataKeeper Cluster Edition configurado de forma que em sincronia reflete conteúdo Olá Olá adicional VHD ligado volume do volume VHD ligado do origem VMs tooadditional de VM de destino.
* SIOS DataKeeper é abstrair volumes locais Olá origem e de destino e apresentá-los tooWindows Cluster de ativação pós-falha como um único disco partilhado.

Pode encontrar todos os detalhes sobre como tooinstall num Cluster de ativação pós-falha do Windows com SIOS Datakeeper e SAP no Olá [Clustering SAP ASCS instância utilizando o Cluster de ativação pós-falha do Windows Server no Azure com SIOS DataKeeper] [ ha-guide-classic]documento técnico.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Elevada disponibilidade para a instância de SAP (A) SCS Olá no Linux
A partir de 2015 Dec também não há nenhum disco tooshared equivalente WSFC para VMs com Linux no Azure. Soluções alternativas utilizando software de terceiros 3rd como SIOS para Windows não são validadas ainda para executar o SAP em Linux no Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Elevada disponibilidade para a instância de base de dados SAP Olá
Olá SAP DBMS HA configuração típica baseia-se em duas VMs de DBMS em que é utilizada a funcionalidade de elevada disponibilidade DBMS dados tooreplicate Olá Active Directory DBMS instância toohello segunda VM numa instância DBMS passiva.

Elevada funcionalidade de recuperação após desastre e disponibilidade para o DBMS no geral, bem como específico DBMS descritas Olá [guia de implementação DBMS][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Elevada disponibilidade de ponto a ponto para Olá sistema SAP completo
Seguem-se dois exemplos concluída SAP NetWeaver HA da arquitetura de no Azure - uma para o Windows e outro para Linux.
conceitos de Olá conforme explicado abaixo poderão ter toobe um pouco comprometido ao implementar vários sistemas de SAP e número de Olá de VMs implementadas está a exceder o limite máximo Olá de contas do Storage por subscrição. Nestes casos, os VHDs das VMs necessário toobe combinado dentro de uma conta de armazenamento. Normalmente, deverá fazê-lo através da combinação de camada de aplicação de VHDs de SAP VMs dos diferentes sistemas SAP.  Podemos também combinadas VHDs diferentes das VMs DBMS diferentes sistemas diferentes de SAP numa conta de armazenamento do Azure. Deste modo, mantendo os limites IOPS Olá de contas do Storage do Azure em mente ( <https://azure.microsoft.com/documentation/articles/storage-scalability-targets> )

##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] HA no Windows
![Arquitetura de HA do SAP NetWeaver aplicações com o SQL Server em IaaS do Azure][planning-guide-figure-3200]

Olá seguir construções do Azure é utilizada para o sistema de SAP NetWeaver Olá, impacto de toominimize por problemas de infraestrutura e o anfitrião de aplicação de patches:

* sistema completo Olá é implementado no Azure (é necessário - Olá, camada DBMS, (A) instância SCS e toorun necessidade de camada de aplicação completa na mesma localização).
* sistema completo Olá é executado dentro de uma subscrição do Azure (obrigatório).
* sistema completo Olá é executado dentro de uma Azure Virtual Network (obrigatório).
* separação de Olá de Olá VMs de um sistema SAP em três conjuntos de disponibilidade é possível mesmo com todas as VMs de Olá pertencente toohello mesma rede Virtual.
* Todas as VMs instâncias em execução DBMS de um sistema SAP estão a ser um conjunto de disponibilidade. Iremos partem do princípio de que não há mais do que um VM a executar instâncias DBMS por sistema desde nativa DBMS elevada disponibilidade funcionalidades são utilizadas, como o AlwaysOn do SQL Server ou o Oracle Data Guard.
* Todas as VMs DBMS instâncias em execução utilizam a sua própria conta de armazenamento. Ficheiros de registo e dados DBMS são replicados a partir de uma conta tooanother armazenamento conta de armazenamento utilizando funções de elevada disponibilidade DBMS que sincronizam os dados de Olá. Indisponibilidade de uma conta de armazenamento fará com que a indisponibilidade de um nó de cluster do Windows do SQL Server, mas não Olá todo serviço do SQL Server.
* Todas as VMs em execução (A) instância SCS de um sistema SAP estão a ser um conjunto de disponibilidade. Dentro dessas VMs é configurar a instância SCS de tooprotect (A) do Windows Sever ativação pós-falha Cluster (WSFC).
* Todas as VMs em execução (A) instâncias SCS utilizam a sua própria conta de armazenamento. (A) Ficheiros de instância do SCS e pasta global SAP são replicadas a partir de uma conta tooanother armazenamento conta de armazenamento utilizando a replicação de SIOS DataKeeper. Indisponibilidade de uma conta de armazenamento fará com que a indisponibilidade de um (A) SCS Windows nó de cluster, mas não Olá todo (A) serviço SCS.
* Todas as VMs de Olá que representa a camada de servidor de aplicação de SAP Olá estão num conjunto de disponibilidade terceiro.
* Todas as VMs de Olá com servidores de aplicações SAP utilizam a sua própria conta de armazenamento. Indisponibilidade de uma conta de armazenamento fará com que a indisponibilidade de um servidor de aplicação de SAP, onde AS outras SAP continuar toorun.

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] HA no Linux
arquitetura de Olá para SAP HA no Linux no Azure é basicamente Olá iguais para o Windows como descrito acima. A partir de Janeiro de 2016 existem apesar dois restrições:

* apenas o SAP ASE 16 é atualmente suportado no Linux no Azure sem quaisquer funcionalidades de replicação ASE.
* Não há nenhuma solução SAP (A) SCS HA ainda suportada no Linux no Azure

Como um consequence de Janeiro de 2016 não é possível alcançar a um sistema de SAP-Linux-Azure Olá mesmo disponibilidade como um sistema de SAP-Windows-Azure devido à falta HA para a instância SCS Olá (A) e o Olá instância única ASE de SAP da base de dados.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Utilizar o início automático para instâncias SAP
SAP oferecidos funcionalidade Olá instâncias SAP toostart imediatamente após o início Olá Olá SO dentro Olá VM. os passos exatos para Olá documentados no artigo da Base de dados de conhecimento SAP [1909114] - como toostart SAP instâncias automaticamente utilizando o parâmetro Autostart. No entanto, SAP é não recomendamos toouse Olá já definição porque não existe nenhum controlo por ordem de Olá de reinícios de instância, partindo do princípio de mais do que uma VM obteve afetada ou foi executada várias instâncias por VM. Partindo do princípio de um cenário típico do Azure de uma instância de servidor de aplicações SAP VM e Olá caso de uma única VM, eventualmente, obter reiniciada, Olá Autostart não está realmente crítico e pode ser ativado adicionando este parâmetro:

    Autostart = 1

Para Olá iniciar o perfil de instância de Olá SAP ABAP e/ou de Java.

> [!NOTE]
> o parâmetro de início automático de Olá pode ter alguns downfalls bem. Em mais detalhe, acionadores de parâmetro de Olá Olá início de uma instância do SAP ABAP ou Java quando Olá relacionados com o serviço do Windows/Linux da instância de Olá foi iniciado. Que certamente se Olá caso de sistemas de operativos Olá efetua o arranque. No entanto, reinícios dos serviços SAP também uma coisa comuns para funcionalidades de gestão de ciclo de vida do Software de SAP como soma ou outras atualizações ou atualiza. Estas funcionalidades não estão à espera um toobe instância reiniciado automaticamente em todos os. Por conseguinte, o parâmetro de Autostart Olá deve ser desativado antes de executar estas tarefas. parâmetro de Autostart Olá também não deve ser utilizado para as instâncias SAP estão agrupados em cluster, como SCS/ASCS/CI.
>
>

Consulte informações adicionais sobre o início automático para SAP instâncias aqui:

* [Iniciar/parar SAP, juntamente com o seu servidor Unix iniciar/parar](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Iniciar e parar os agentes de gestão do SAP NetWeaver](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Como tooenable auto iniciar da base de dados HANA](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Maior sistemas SAP de 3 camadas
Aspetos de elevada disponibilidade das configurações de SAP de 3 camadas já obteve abordados nas secções anteriores. Mas que sobre os sistemas onde são demasiado grandes requisitos do servidor Olá DBMS toohave localizado no Azure, mas a camada da aplicação Olá SAP pode ser implementada no Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Localização das configurações de SAP de 3 camadas
Não é suportado toosplit Olá a camada da aplicação em si ou aplicação Olá e DBMS camada entre no local e o Azure. Um sistema SAP está totalmente implementado no local ou no Azure. Também não é suportado toohave alguns dos servidores de aplicação Olá ser executado no local e outros no Azure. É Olá ponto de debate Olá de partida. Iremos também são não suporta componentes DBMS Olá toohave de um sistema SAP e Olá camada de servidor de aplicação de SAP implementada em duas regiões do Azure diferente. Por exemplo, DBMS na camada de aplicação EUA oeste e SAP nos EUA Central. Motivo para não suportar a essas configurações é sensibilidade de latência de Olá dos Olá SAP NetWeaver arquitetura.

No entanto, decorrer Olá dos dados de último ano parceiros center desenvolvidas localizações conjunta tooAzure regiões. Estas localizações conjunta são, muitas vezes, dados do Azure físicos muito perto toohello centros dentro de uma região do Azure. distância curto Olá e ligação de recursos de localização conjunta Olá através do ExpressRoute para o Azure podem resultar numa latência que é inferior a 2ms. Nestes casos, é possível toolocate Olá DBMS layer (incluindo o armazenamento SAN/NAS) em colocalização e camada da aplicação Olá SAP no Azure. A partir de Dec de 2015, não temos todas as implementações que assim o desejar. Mas diferentes clientes com implementações de aplicações SAP não estiver a utilizar já essas abordagens.

### <a name="offline-backup-of-sap-systems"></a>Sistemas de cópia de segurança do SAP offline
Depende de Olá SAP escolhida (camada 2 ou 3 camadas) existe foi possível configuração toobackup uma necessidade. Olá conteúdo Olá própria VM plus toohave uma cópia de segurança da base de dados de Olá. Olá DBMS relacionadas com cópias de segurança esperada toobe feito com métodos de base de dados. Uma descrição detalhada para bases de dados diferente de Olá, pode ser encontrado na [DBMS guia][dbms-guide]. No Olá por outro lado, Olá dados SAP pode ser feita de forma offline (incluindo, bem como o conteúdo da base de dados Olá) conforme descrito nesta secção ou online, tal como descrito na secção seguinte, Olá.

cópia de segurança offline Olá basicamente precisaria que um encerramento de Olá VM através do Portal do Azure de Olá e uma cópia de disco da VM base Olá plus todas ligada VHDs toohello VM. Isto seria preservar um ponto na imagem de tempo de Olá VM e o respetivo disco associado. É recomendado toocopy Olá 'as cópias de segurança' para uma conta de armazenamento do Azure diferente. Olá, por conseguinte, o procedimento descrito em capítulo [copiar os discos entre contas de armazenamento do Azure] [ planning-guide-5.4.2] deste documento seria aplicada.
Além das Olá encerramento utilizando Olá Portal do Azure, um pode também fazê-lo através do Powershell ou o CLI conforme descrito aqui: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Um restauro de estado do que seria consistir eliminar Olá base VM, bem como discos original Olá Olá base VM e montado VHDs, copiar Olá back guardado VHDs toohello conta do Storage original e implementando Olá sistema.
Este artigo mostra um exemplo de como tooscript este processo no Powershell: <http://www.westerndevs.com/azure-snapshots/>

Certifique-se tooinstall uma licença nova do SAP, uma vez que restoing uma cópia de segurança VM, tal como descrito acima cria uma nova chave de hardware.

### <a name="online-backup-of-an-sap-system"></a>Cópia de segurança online de um sistema SAP
É efetuada cópia de segurança de Olá DBMS com métodos específicos DBMS, conforme descrito em Olá [DBMS guia][dbms-guide].

Outras VMs dentro Olá sistema SAP podem ser feitas utilizando a funcionalidade de cópia de segurança do Azure Máquina Virtual. Cópia de segurança de Máquina Virtual do Azure foi introduzida no início de 2015 e entretanto é um método padrão toobackup uma VM no Azure completa. Cópia de segurança do Azure armazena cópias de segurança de Olá no Azure e permite que um restauro de uma VM.

> [!NOTE]
> A partir de 2015 Dec utilizando a cópia de segurança de VM não manter Olá VM um ID exclusivo que é utilizado para SAP licenciamento. Isto significa que um restauro a partir de uma cópia de segurança VM requer a instalação de uma nova chave de licença SAP Olá restaurado VM é considerada toobe uma nova VM e não uma substituição de um anteriores que foi guardado.
> A partir de Janeiro de 2016 cópia de segurança do Azure ainda não suporta VMs que são implementadas com o Azure Resourc Manager.
>
> ![Windows][Logo_Windows] Windows
>
> Teoria VMs que bases de dados de execução podem ser feitas de forma consistente, bem como se Olá DBMS sistemas suporta Olá Windows VSS (serviço de cópia sombra de volumes <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx > ) como, por exemplo, o servidor de SQL não.
> No entanto, tenha em atenção de que com base em cópias de segurança de VM do Azure no momento restaura das bases de dados não são possíveis. Por conseguinte, a recomendação é tooperform cópias de segurança das bases de dados com a funcionalidade DBMS em vez de depender de cópia de segurança do Azure
>
> tooget familiarizado com a cópia de segurança do Azure Máquina Virtual inicie aqui: <https://azure.microsoft.com/documentation/articles/backup-azure-vms/>.
>
> Outras possibilidades são toouse uma combinação do Microsoft Data Protection Manager instalada numa VM do Azure e cópia de segurança do Azure para bases de dados de cópia de segurança/restauro. Podem encontrar mais informações aqui: <https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction/>.  
>
> ![Linux][Logo_Linux] Linux
>
> Não há nenhum equivalente tooWindows VSS no Linux. Por conseguinte, apenas as cópias de segurança consistente com ficheiros estão possíveis mas não consistentes com aplicações cópias de segurança. Olá cópia de segurança do SAP DBMS deve ser feita utilizando a funcionalidade DBMS. Olá sistema de ficheiros que inclui Olá SAP relacionadas com a dados podem ser guardados, por exemplo, utilizando tar conforme descrito aqui: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure como site de DR para landscapes SAP de produção
Desde Mid 2014, os componentes de toovarious extensões em torno do Hyper-V, o System Center e o Azure ativar Olá da utilização do Azure como site de DR para VMs em execução no local com base no Hyper-V.

Um blogue com detalhes sobre como toodeploy esta solução é documentados aqui: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>

## <a name="summary"></a>Resumo
Olá pontos-chave do elevada disponibilidade para sistemas SAP no Azure são:

* Neste ponto no tempo, Olá ponto único de SAP de falha não pode ser protegida exatamente Olá igual a forma como pode ser feita em implementações no local. motivo Olá é que os clusters de disco partilhado ainda não podem ser criados no Azure, sem utilização Olá 3rd software de terceiros.
* Para a camada DBMS Olá precisa de funcionalidade DBMS toouse que não depende da tecnologia de cluster de disco partilhado. Detalhes estão documentados na Olá [DBMS guia][dbms-guide].
* impacto de Olá toominimize dos problemas dentro de domínios de falhas no Olá manutenção de anfitrião ou de infraestrutura do Azure, deve utilizar conjuntos de disponibilidade do Azure:
  * Recomenda-se toohave um conjunto de disponibilidade para a camada da aplicação Olá SAP.
  * É recomendado toohave uma disponibilidade separada definida para a camada de SAP DBMS Olá.
  * Não é recomendado Olá tooapply que do conjunto de disponibilidade do mesma para as VMs de sistemas SAP diferentes.
* Para fins de cópia de segurança de camada de SAP DBMS Olá, verifique Olá [DBMS guia][dbms-guide].
* Cópia de segurança de instâncias de caixa de diálogo de SAP só faz sentido pouca porque se trata de instâncias de caixa de diálogo simples tooredeploy normalmente mais rápidas.
* Cópia de segurança Olá VM que contém o diretório de global Olá de Olá sistema SAP e com todos os perfis de Olá de instâncias diferentes do Olá, fazer sentido e deve ser efetuada com cópia de segurança do Windows ou por ex. tar no Linux. Uma vez que existem diferenças entre o Windows Server 2008 (R2) e Windows Server 2012 (R2), que torna mais fácil toobackup Olá mais recente a utilizar versões do Windows Server, recomendamos toorun do Windows Server 2012 (R2) como sistema operativo Windows.
