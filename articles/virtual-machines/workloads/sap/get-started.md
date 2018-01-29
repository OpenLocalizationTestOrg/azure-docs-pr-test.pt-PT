---
title: "Introdução ao SAP em VMs do Azure | Microsoft Docs"
description: "Saiba mais sobre as soluções SAP em execução em máquinas virtuais (VMs) no Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/02/2018
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a0dcb941db5038b7c904c9eaa8599c5a1dc6e83
ms.sourcegitcommit: 2e540e6acb953b1294d364f70aee73deaf047441
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/03/2018
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a>Utilizar o Azure para alojar e executar cenários de carga de trabalho SAP
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

[dbms-guide]:dbms-guide.md
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8
[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md
[ha-guide-get-started]:sap-high-availability-guide-start.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../windows/premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../linux/multiple-nics.md
[virtual-network-deploy-multinic-arm-ps]:../windows/multiple-nics.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-network-deploy-multinic-classic-ps.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

Ao escolher o Microsoft Azure como o parceiro de nuvem pronto SAP, conseguir executar fiável o missão críticas SAP as cargas de trabalho e cenários numa plataforma em conformidade, dimensionável e comprovada de empresa.  Obtenha a escalabilidade, a flexibilidade e a redução de custos do Azure. Com a expandido parceria entre o Microsoft e SAP, pode executar aplicações SAP em cenários de desenvolvimento/teste e produção no Azure - e serem totalmente suportadas. Do SAP NetWeaver SAP S4/HANA, BI do SAP, Linux para o Windows, SAP HANA para SQL Server, temos de que abrange.

Para além de cenários do SAP NetWeaver com o DBMS diferentes no Azure de alojamento, pode alojar diferentes outros cenários de carga de trabalho SAP, como o SAP BI no Azure. Pode encontrar documentação sobre implementações de SAP NetWeaver em máquinas virtuais nativo do Azure na secção "SAP NetWeaver em máquinas virtuais do Azure".

O Azure tem nativo ofertas de Máquina Virtual do Azure que nunca estão a crescer num tamanho de recursos de CPU e memória para cobrir SAP a carga de trabalho tira partido do SAP HANA. Para obter mais informações sobre este tópico, procure os documentos na secção em Azure Virtual Machines do SAP HANA."

A exclusividade do Azure para SAP HANA é uma oferta exclusiva que define o Azure para além dos concorrência. Para poder ativar o alojamento mais recursos de CPU e memória SAP pedir o seu trabalho cenários que envolvem SAP HANA, o Azure oferece a utilização do cliente dedicada hardware bare-metal para fins de estiverem a executar implementações de SAP HANA que necessitam de até 20 TB (escalável 60 TB) de memória de S/4HANA ou outras cargas de trabalho de SAP HANA. Esta solução do Azure exclusiva de SAP HANA no Azure (instâncias de grande) permite-lhe executar SAP HANA no hardware dedicado bare-metal com o SAP aplicação camada ou carga de trabalho meio-ware maligno alojado no nativo máquinas virtuais do Azure. Esta solução é descrita em vários documentos na secção "SAP HANA no Azure (instâncias de grande)".   

Cenários de carga de trabalho SAP no Azure de alojamento também podem criar requisitos de integração de identidade e Single-Sign-On com o diretório de atividade do Azure para os diferentes componentes SAP e SAP SaaS ou PaaS oferece. Uma lista de integração e a Single-Sign-On cenários com o Azure Active Directory (AAD) e SAP entidades é descrita e documentada na secção "integração de identidade do AAD SAP e Single-Sign-On."


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a>SAP HANA no SAP HANA no Azure (instâncias de grandes)

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a>Descrição geral e arquitetura de SAP HANA no Azure (instâncias de grandes)
Título: Descrição geral e arquitetura de SAP HANA no Azure (instâncias de grandes)

Resumo: Esta arquitetura e o guia de implementação técnica fornece informações para ajudar a implementar SAP no SAP HANA novo no Azure (instâncias de grande) no Azure. Não se destina a ser um guia abrangente que abrangem configuração específica de soluções SAP, mas em vez disso útil informações na sua implementação inicial e as operações em curso. Não, deve substituir documentação SAP relacionadas com a instalação de SAP HANA (ou as notas de suporte de SAP muitos que abrangem o tópico). Isto dá-lhe uma descrição geral e fornece o detalhes adicionais sobre a instalação de SAP HANA no Azure (instâncias de grande).

Atualizada: De Outubro de 2017

[Este guia pode ser encontrado aqui](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-to-sap-hana-on-azure-large-instances"></a>Infraestrutura e de conectividade para SAP HANA no Azure (instâncias de grandes)
Título: Infraestrutura e conectividade para SAP HANA no Azure (instâncias de grandes)

Resumo: Após a compra de SAP HANA no Azure (instâncias de grande) está finalizada entre si e a equipa da conta Microsoft enterprise, são necessárias várias configurações de rede para garantir a conectividade adequada.  Este documento descreve as informações que tem de ser partilhados com as seguintes informações são necessárias. Este documento descreve as informações que tem de ser recolhidos e que os scripts de configuração têm de ser executado.

Atualizada: De Outubro de 2017

[Este guia pode ser encontrado aqui](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a>Instalar o SAP HANA SAP HANA no Azure (instâncias de grandes)
Título: Instale SAP HANA SAP HANA no Azure (instâncias de grandes)

Resumo: Este documento descreve os procedimentos de configuração para instalar o SAP HANA na sua instância de grande de Azure.

Atualizadas: de 2017 de Julho

[Este guia pode ser encontrado aqui](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a>Elevada disponibilidade e recuperação após desastre de SAP HANA no Azure (instâncias de grandes)
Título: Elevada disponibilidade e recuperação após desastre de SAP HANA no Azure (instâncias de grandes)

Resumo: Elevada disponibilidade (ed) e recuperação após desastre (DR) são muito importantes aspetos da sua SAP HANA fundamentais a ser executado no servidor (es) do Azure (instâncias de grande). -'S importação para trabalhar com o SAP, sua integrador de sistema e/ou Microsoft corretamente architect e implementar o direito de estratégia HA/DR para si. Considerações importantes sobre como o objetivo de ponto de recuperação (RPO) e recuperação tempo objetivo (RTO), específicos ao seu ambiente, tem de ser considerada.  Este documento explica as opções para ativar o nível preferencial de HA e DR.

Atualizada: De Outubro de 2017

[Este documento pode ser encontrado aqui](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a>Resolução de problemas e a monitorização de SAP HANA no Azure (instâncias de grandes)
Título: Resolução de problemas e a monitorização de SAP HANA no Azure (instâncias de grandes)

Resumo: Este guia aborda informações que são úteis para estabelecer a monitorização do seu SAP HANA no ambiente do Azure, bem como informações de resolução de problemas adicionais.

Atualizada: De Outubro de 2017

[Este documento pode ser encontrado aqui](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a>SAP HANA nas Máquinas Virtuais do Azure

### <a name="getting-started-with-sap-hana-on-azure"></a>Introdução ao SAP HANA no Azure
Título: Guia de introdução para instalação manual de SAP HANA em VMs do Azure

Resumo: Neste guia de introdução ajuda a configurar um sistema de SAP HANA instância única em VMs do Azure por uma instalação manual do SAP NetWeaver 7.5 e SP12 do SAP HANA. O guia presumes que o leitor está familiarizado com as noções básicas do IaaS do Azure como como implementar máquinas virtuais e as redes virtuais ou através do portal do Azure ou/CLI do Powershell, incluindo a opção para utilizar modelos json. Além disso, é esperado que o leitor está familiarizado com o SAP HANA, SAP NetWeaver e como o instalar no local.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a>Implementação de SAP CAL de S/4HANA no Azure
Título: Implementar SAP S/4HANA ou BW/4HANA no Azure

Resumo: Este guia ajuda para demonstrar a implementação de SAP S/4HANA no Azure utilizando a biblioteca de dispositivo do SAP na nuvem. Biblioteca de dispositivo do SAP na nuvem é um serviço por SAP que lhe permite implementar aplicações SAP no Azure. O guia passo a passo descreve a implementação.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a>Elevada disponibilidade de SAP HANA em máquinas virtuais do Azure
Título: Elevada disponibilidade de SAP HANA em máquinas virtuais do Azure

Resumo: Este guia descreve a configuração de elevada disponibilidade do SUSE 12 SO e SAP HANA para acomodar a replicação do sistema de HANA com ativação pós-falha automática. O guia é específico para SUSE e Virtual Machines do Azure. O guia aplicável ainda Red Hat ou bare-metal ou privada nuvem ou outras implementações de nuvem pública não do Azure.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a>Descrição geral de cópia de segurança SAP HANA em VMs do Azure
Título: Guia a cópia de segurança para SAP HANA em Azure Virtual Machines

Resumo: Este guia fornece informações básicas sobre as possibilidades de cópia de segurança SAP HANA no Azure máquinas virtuais em execução.

Atualizadas: Março de 2017

[Este guia pode ser encontrado aqui](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a>Backup de nível de ficheiro de SAP HANA em VMs do Azure
Título: Cópia de segurança do SAP HANA com base nos instantâneos de armazenamento

Resumo: Este guia fornece informações sobre como utilizar cópias de segurança baseadas em instantâneos em VMs do Azure ao executar em Azure Virtual Machines de SAP HANA.

Atualizadas: Março de 2017

[Este guia pode ser encontrado aqui](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a>Instantâneo de SAP HANA cópias de segurança com base em VMs do Azure
Título: SAP HANA Azure Backup no nível de ficheiro

Resumo: Este guia fornece informações sobre como utilizar o backup de nível de ficheiro de SAP HANA SAP HANA no Azure máquinas virtuais em execução

Atualizadas: Março de 2017

[Este guia pode ser encontrado aqui](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>NetWeaver SAP implementado em Azure Virtual Machines

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a>Implementar o sistema SAP IDES no Windows e o SQL Server através de CAL SAP no Azure
Título: Testar o SAP NetWeaver em VMs do Microsoft Azure SUSE Linux

Resumo: Este documento descreve a implementação de um sistema SAP IDES com base no Windows e o SQL Server no Azure utilizando a biblioteca de dispositivo do SAP na nuvem. Aplicação de nuvem do SAP biblioteca é um serviço SAP que permite que a implementação dos produtos SAP no Azure. Este documento vai passo a passo através da implementação de um sistema SAP IDES. O sistema IDES é apenas um exemplo para várias outras dozen aplicações que podem ser implementadas através de aplicação de nuvem de SAP no Microsoft Azure.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a>Guia de início rápido para NetWeaver no SUSE Linux no Azure
Título: Testar o SAP NetWeaver em VMs do Microsoft Azure SUSE Linux

Resumo: Este artigo descreve vários aspetos a considerar quando estiver a executar o SAP NetWeaver em máquinas virtuais do Microsoft Azure SUSE Linux (VMs). SAP NetWeaver é oficialmente suportado no SUSE Linux VMs no Azure. Todos os detalhes sobre as versões de Linux, as versões do SAP kernel e outros detalhes podem ser encontrados na 1928533 de nota SAP "aplicações SAP no Azure: suportada produtos e os tipos VM do Azure".

Atualizada: De Setembro de 2016

[Este guia pode ser encontrado aqui](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planeamento e implementação
Título: Máquinas virtuais do Azure, planeamento e implementação de SAP NetWeaver

Resumo: Este documento é o guia de começar com se estiver a pensar sobre como executar SAP NetWeaver em Azure Virtual Machines. Este guia de planeamento e implementação ajuda-o a avaliar se um sistema existente ou planeado, com base em SAP NetWeaver pode ser implementado num ambiente Virtual Machines do Azure. Aborda os vários cenários de implementação do SAP NetWeaver e inclui configurações SAP, que são específicas para o Azure. O documento apresenta e descreve todas as configurações necessárias informações que terá no lado SAP/Azure para executar uma versão híbrida horizontal SAP. As medidas que pode tomar para garantir elevada disponibilidade dos sistemas baseados em SAP NetWeaver no IaaS também estão abrangidas.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui][planning-guide]

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a>Elevada disponibilidade as configurações do SAP NetWeaver em VMs do Azure
Título: Máquinas virtuais do Azure elevada disponibilidade para SAP NetWeaver

Resumo: Neste documento, vamos abordar os passos que pode efetuar para implementar sistemas SAP de elevada disponibilidade no Azure utilizando o modelo de implementação Azure Resource Manager. Vamos guiá-lo estas tarefas principais. O documento, vamos descrevem como único-ponto-de-falhas componentes, como o Advanced negócio Application Programming (ABAP) SAP Central serviços (ASCS) / SAP Central serviços (SCS) e sistemas de gestão de base de dados (DBMS) e os componentes redundantes, como o servidor de aplicações SAP que vão ser protegidos quando em execução em VMs do Azure. Um exemplo passo a passo de uma instalação e configuração de um sistema SAP de elevada disponibilidade num cluster de Clustering de ativação pós-falha do Windows Server e SUSE Linux Enterprise Server Cluster Framework no Azure é demonstrado e apresentado neste documento.

Atualizada: De Outubro de 2017

[Este guia pode ser encontrado aqui][ha-guide-get-started]

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a>Compreender o SID de várias implementações do SAP NetWeaver em VMs do Azure
Título: Criar uma configuração de várias SID do SAP NetWeaver

Resumo: Este documento é um complemento o documento de elevada disponibilidade para SAP NetWeaver em VMs do Azure. Devido à nova funcionalidade no Azure que foi introduzida em Setembro de 2016, é possível implementar várias instâncias do SAP NetWeaver ASCS/SCS num par de VMs do Azure. Com a configuração, pode reduzir o número de VMs necessários para implementar para elevada SAP NetWeaver configurações. O guia descreve a configuração dessas configurações de várias SID.

Atualizada: De Dezembro de 2016

[Este guia pode ser encontrado aqui](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Implementação do SAP NetWeaver em VMs do Azure
Título: Implementação de máquinas virtuais do Azure para SAP NetWeaver

Resumo: Este documento dispõe de documentação de orientação sobre procedimentos para implementar software SAP NetWeaver em máquinas virtuais no Azure. Este documento concentra-se em três cenários de implementação específicos, com destaque na ativação das Extensões de Monitorização do Azure para SAP, incluindo recomendações da resolução de problemas para as Extensões de Monitorização do Azure para SAP. Este documento parte do princípio de que leu o guia de planeamento e implementação.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui][deployment-guide]

### <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guia de implementação DBMS
Título: Implementação DBMS de máquinas virtuais do Azure para SAP NetWeaver

Resumo: Este documento aborda considerações de planeamento e implementação para os sistemas DBMS que devem ser executados em conjunto com o SAP. Na primeira parte, as considerações gerais estão listadas e apresentadas. As partes seguintes do documento relacionam-se com implementações de diferentes DBMS no Azure que são suportadas pelo SAP. Diferentes DBMS apresentados são do SQL Server, SAP ASE e Oracle. Nessas partes específicas, as considerações a que ter para a conta para quando estiver a executar sistemas SAP no Azure em conjunto com essas DBMS são debatidas. Os assuntos como métodos de cópia de segurança e de elevada disponibilidade que são suportados pelos diferentes DBMS no Azure são apresentados para utilização com as aplicações SAP.

Atualizadas: Junho de 2017

[Este guia pode ser encontrado aqui][dbms-guide]

### <a name="using-azure-site-recovery-for-sap-workload"></a>Utilizar o Azure Site Recovery para a carga de trabalho do SAP
Título: SAP NetWeaver: criar uma solução de recuperação após desastre com o Azure Site Recovery

Resumo: Este documento descreve a forma como os serviços do Azure Site Recovery podem ser utilizados para fins de processamento de cenários de recuperação após desastre. Casos onde Azure é utilizado como localização de recuperação de desastres para um horizontal SAP no local utilizando o Azure Site Recovery Services. Outro cenário descrito no documento é o cenário de recuperação de desastre do Azure para o Azure (A2A) e como são gerido com o Azure Site Recovery.  

Atualizadas: Agosto de 2017

[Este guia pode ser encontrado aqui](http://aka.ms/asr-sap)
