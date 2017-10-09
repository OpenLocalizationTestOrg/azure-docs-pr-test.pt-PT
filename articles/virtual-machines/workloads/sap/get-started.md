---
title: "aaaGetting começar SAP em VMs do Azure | Microsoft Docs"
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
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a><span data-ttu-id="1ea57-103">Utilizar o Azure para alojar e executar cenários de carga de trabalho SAP</span><span class="sxs-lookup"><span data-stu-id="1ea57-103">Using Azure for hosting and running SAP workload scenarios</span></span>
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
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
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
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
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

<span data-ttu-id="1ea57-104">Ao escolher o Microsoft Azure como o parceiro de nuvem pronto SAP, são tooreliably capaz de executar o missão críticas SAP as cargas de trabalho e cenários numa plataforma em conformidade, dimensionável e comprovada de empresa.</span><span class="sxs-lookup"><span data-stu-id="1ea57-104">By choosing Microsoft Azure as your SAP ready cloud partner, you are able tooreliably run your mission critical SAP workloads and scenarios on a scalable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="1ea57-105">Obter escalabilidade Olá, flexibilidade e o custo reduções do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-105">Get hello scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="1ea57-106">Com Olá expandido parceria entre a Microsoft e SAP, pode executar aplicações SAP em cenários de desenvolvimento/teste e produção no Azure - e serem totalmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="1ea57-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in Azure - and be fully supported.</span></span> <span data-ttu-id="1ea57-107">Do SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, tooSQL de SAP HANA, temos de que abrange.</span><span class="sxs-lookup"><span data-stu-id="1ea57-107">From SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="1ea57-108">Para além de cenários do SAP NetWeaver com de alojamento Olá DBMS diferentes no Azure, pode alojar diferentes outros cenários de carga de trabalho SAP, como o SAP BI no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-108">Besides hosting SAP NetWeaver scenarios with hello different DBMS on Azure, you can host different other SAP workload scenarios, like SAP BI on Azure.</span></span> <span data-ttu-id="1ea57-109">Pode encontrar documentação sobre implementações de SAP NetWeaver em máquinas virtuais nativo do Azure na secção de Olá "SAP NetWeaver em máquinas virtuais do Azure".</span><span class="sxs-lookup"><span data-stu-id="1ea57-109">Documentation regarding SAP NetWeaver deployments on Azure native Virtual Machines can be found in hello section "SAP NetWeaver on Azure Virtual Machines."</span></span> 

<span data-ttu-id="1ea57-110">O Azure tem nativo ofertas de Máquina Virtual do Azure que nunca estão a crescer num tamanho de memória e CPU recursos toocover SAP carga de trabalho que tira partido do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ea57-110">Azure has native Azure Virtual Machine offers that are ever growing in size of CPU and memory resources toocover SAP workload that leverages SAP HANA.</span></span> <span data-ttu-id="1ea57-111">Para obter mais informações sobre este tópico, procurar documentos Olá na secção de Olá em Azure Virtual Machines do SAP HANA."</span><span class="sxs-lookup"><span data-stu-id="1ea57-111">For more information on this topic, look up hello documents under hello section SAP HANA on Azure Virtual Machines."</span></span>

<span data-ttu-id="1ea57-112">exclusividade Olá do Azure para SAP HANA é uma oferta exclusiva que define o Azure para além dos concorrência.</span><span class="sxs-lookup"><span data-stu-id="1ea57-112">hello uniqueness of Azure for SAP HANA is a unique offer that sets Azure apart from competition.</span></span> <span data-ttu-id="1ea57-113">No tooenable de ordem de alojamento mais recursos de CPU e memória SAP pedir o seu trabalho cenários que envolvem SAP HANA, o Azure oferece utilização hello do cliente dedicado hardware bare-metal para efeitos de Olá de implementações de SAP HANA que requerem too20 TB (escalável 60 TB) de cópia de segurança em execução memória de S/4HANA ou outras cargas de trabalho de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ea57-113">In order tooenable hosting more memory and CPU resource demanding SAP scenarios involving SAP HANA, Azure offers hello usage of customer dedicated bare-metal hardware for hello purpose of running SAP HANA deployments that require up too20 TB (60 TB scale-out) of memory for S/4HANA or other SAP HANA workload.</span></span> <span data-ttu-id="1ea57-114">Esta solução do Azure exclusiva de SAP HANA no Azure (instâncias de grande) permite-lhe toorun SAP HANA no hardware de bare-metal Olá dedicado com Olá SAP aplicação camada ou carga de trabalho meio-ware maligno alojado no nativo máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-114">This unique Azure solution of SAP HANA on Azure (Large Instances) allows you toorun SAP HANA on hello dedicated bare-metal hardware with hello SAP application layer or workload middle-ware layer hosted in native Azure Virtual Machines.</span></span> <span data-ttu-id="1ea57-115">Esta solução é descrita em vários documentos na secção de Olá "SAP HANA no Azure (instâncias de grande)".</span><span class="sxs-lookup"><span data-stu-id="1ea57-115">This solution is documented in several documents in hello section "SAP HANA on Azure (Large Instances)."</span></span>   

<span data-ttu-id="1ea57-116">Cenários de carga de trabalho SAP no Azure de alojamento também podem criar requisitos de integração de identidade e Single-Sign-On utilizar componentes SAP toodifferent de diretório de atividade do Azure e do SaaS SAP ou PaaS oferece.</span><span class="sxs-lookup"><span data-stu-id="1ea57-116">Hosting SAP workload scenarios in Azure also can create requirements of Identity integration and Single-Sign-On using Azure Activity Directory toodifferent SAP components and SAP SaaS or PaaS offers.</span></span> <span data-ttu-id="1ea57-117">Uma lista de integração e a Single-Sign-On cenários com o Azure Active Directory (AAD) e SAP entidades é descrita e documentada na secção de Olá "integração de identidade do AAD SAP e Single-Sign-On."</span><span class="sxs-lookup"><span data-stu-id="1ea57-117">A list of such integration and Single-Sign-On scenarios with Azure Active Directory (AAD) and SAP entities is described and documented in hello section "AAD SAP Identity Integration and Single-Sign-On."</span></span>


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-118">SAP HANA no SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-118">SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-119">Descrição geral e arquitetura de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="1ea57-120">Título: aaaOverview e arquitetura de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-120">title: aaaOverview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="1ea57-121">Resumo: Esta arquitetura e o guia de implementação técnica fornece toohelp informações implementar SAP no Olá novo SAP HANA no Azure (instâncias de grande) no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-121">Summary: This Architecture and Technical Deployment Guide provides information toohelp you deploy SAP on hello new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="1ea57-122">Não é uma configuração específica do abrangente guia abrangente de soluções SAP, mas em vez disso útil informações na sua implementação inicial e as operações em curso de toobe pretendido.</span><span class="sxs-lookup"><span data-stu-id="1ea57-122">It is not intended toobe a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="1ea57-123">Não deve substituir o documentação SAP relacionadas com a instalação de toohello de SAP HANA (ou Olá muitos notas de suporte de SAP que abrangem tópico Olá).</span><span class="sxs-lookup"><span data-stu-id="1ea57-123">It should not replace SAP documentation related toohello installation of SAP HANA (or hello many SAP Support Notes that cover hello topic).</span></span> <span data-ttu-id="1ea57-124">Fornece uma descrição geral e fornece Olá detalhes adicionais sobre a instalação de SAP HANA no Azure (instâncias de grande).</span><span class="sxs-lookup"><span data-stu-id="1ea57-124">It gives you an overview and provides hello additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="1ea57-125">Atualizadas: de 2017 de Julho</span><span class="sxs-lookup"><span data-stu-id="1ea57-125">Updated: July 2017</span></span>

[<span data-ttu-id="1ea57-126">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-127">Infraestrutura e a conectividade tooSAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-127">Infrastructure and connectivity tooSAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="1ea57-128">Título: aaaInfrastructure e conectividade tooSAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-128">title: aaaInfrastructure and Connectivity tooSAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="1ea57-129">Resumo: Após a compra de Olá de SAP HANA no Azure (instâncias de grande) está finalizada entre si e Olá equipa da conta Microsoft enterprise, diversas configurações de rede são necessários na conectividade adequada de tooensure de ordem.</span><span class="sxs-lookup"><span data-stu-id="1ea57-129">Summary: After hello purchase of SAP HANA on Azure (Large Instances) is finalized between you and hello Microsoft enterprise account team, various network configurations are required in order tooensure proper connectivity.</span></span>  <span data-ttu-id="1ea57-130">Estes informações Olá destaca de documento que tenha toobe partilhado com Olá seguintes informações são necessárias.</span><span class="sxs-lookup"><span data-stu-id="1ea57-130">This document outlines hello information that has toobe shared with hello following information is required.</span></span> <span data-ttu-id="1ea57-131">Este documento descreve as informações que tem toobe recolhidos e os scripts de configuração tem toobe executar.</span><span class="sxs-lookup"><span data-stu-id="1ea57-131">This document outlines what information has toobe collected and what configuration scripts have toobe run.</span></span> 

<span data-ttu-id="1ea57-132">Atualizadas: de 2017 de Julho</span><span class="sxs-lookup"><span data-stu-id="1ea57-132">Updated: July 2017</span></span>

[<span data-ttu-id="1ea57-133">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-134">Instalar o SAP HANA SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-134">Install SAP HANA in SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="1ea57-135">Título: aaaInstall SAP HANA no SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-135">title: aaaInstall SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="1ea57-136">Resumo: Este documento descreve os procedimentos de configuração de Olá para instalar o SAP HANA na sua instância de grande de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-136">Summary: This document outlines hello setup procedures for installing SAP HANA on your Azure Large Instance.</span></span> 

<span data-ttu-id="1ea57-137">Atualizadas: de 2017 de Julho</span><span class="sxs-lookup"><span data-stu-id="1ea57-137">Updated: July 2017</span></span>

[<span data-ttu-id="1ea57-138">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-139">Elevada disponibilidade e recuperação após desastre de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="1ea57-140">Título: aaaHigh disponibilidade e após desastre de recuperação de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-140">title: aaaHigh Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="1ea57-141">Resumo: Elevada disponibilidade (ed) e recuperação após desastre (DR) são muito importantes aspetos da sua SAP HANA fundamentais a ser executado no servidor (es) do Azure (instâncias de grande).</span><span class="sxs-lookup"><span data-stu-id="1ea57-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="1ea57-142">De importação toowork com SAP, sua integrador de sistema e/ou Microsoft tooproperly architect e implementa direito Olá HA/DR estratégia para si.</span><span class="sxs-lookup"><span data-stu-id="1ea57-142">It's import toowork with SAP, your system integrator, and/or Microsoft tooproperly architect and implement hello right HA/DR strategy for you.</span></span> <span data-ttu-id="1ea57-143">Considerações importantes sobre como o objetivo de ponto de recuperação (RPO) e o objetivo de tempo de recuperação (RTO), ambiente de tooyour específico, tem de ser considerada.</span><span class="sxs-lookup"><span data-stu-id="1ea57-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific tooyour environment, must be considered.</span></span>  <span data-ttu-id="1ea57-144">Este documento explica as opções para ativar o nível preferencial de HA e DR.</span><span class="sxs-lookup"><span data-stu-id="1ea57-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="1ea57-145">Atualizada: De Dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="1ea57-145">Updated: December 2016</span></span>

[<span data-ttu-id="1ea57-146">Este documento pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1ea57-147">Resolução de problemas e a monitorização de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="1ea57-148">Título: aaaTroubleshooting e monitorização de SAP HANA no Azure (instâncias de grandes)</span><span class="sxs-lookup"><span data-stu-id="1ea57-148">title: aaaTroubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="1ea57-149">Resumo: Este guia aborda informações que são úteis para estabelecer a monitorização do seu SAP HANA no ambiente do Azure, bem como informações de resolução de problemas adicionais.</span><span class="sxs-lookup"><span data-stu-id="1ea57-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="1ea57-150">Atualizada: De Dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="1ea57-150">Updated: December 2016</span></span>

[<span data-ttu-id="1ea57-151">Este documento pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a><span data-ttu-id="1ea57-152">SAP HANA nas Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-152">SAP HANA on Azure Virtual Machines</span></span>

### <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="1ea57-153">Introdução ao SAP HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-153">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="1ea57-154">Título: aaaQuickstart guia de instalação manual de SAP HANA em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-154">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="1ea57-155">Resumo: Neste guia de introdução ajuda-o tooset um sistema de SAP HANA instância única em VMs do Azure por uma instalação manual do SAP NetWeaver 7.5 e SP12 do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ea57-155">Summary: This quickstart guide helps tooset up a single-instance SAP HANA system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="1ea57-156">Guia de Olá presumes que leitor Olá está familiarizado com as noções básicas do IaaS do Azure como como máquinas de virtuais toodeploy ou redes virtuais por Olá portal do Azure ou a CLI do Powershell, incluindo por Olá modelos do opção toouse json.</span><span class="sxs-lookup"><span data-stu-id="1ea57-156">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="1ea57-157">Além disso, é esperado que o leitor de Olá está familiarizado com o SAP HANA, SAP NetWeaver e como tooinstall-lo no local.</span><span class="sxs-lookup"><span data-stu-id="1ea57-157">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="1ea57-158">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-158">Updated: June 2017</span></span>

[<span data-ttu-id="1ea57-159">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-159">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a><span data-ttu-id="1ea57-160">Implementação de SAP CAL de S/4HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-160">S/4HANA SAP CAL deployment on Azure</span></span>
<span data-ttu-id="1ea57-161">Título: aaaDeploy SAP S/4HANA ou BW/4HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-161">title: aaaDeploy SAP S/4HANA or BW/4HANA on Azure</span></span>

<span data-ttu-id="1ea57-162">Resumo: Este guia ajuda-o de implementação Olá toodemonstrate SAP S/4HANA no Azure utilizando a biblioteca de dispositivo do SAP na nuvem.</span><span class="sxs-lookup"><span data-stu-id="1ea57-162">Summary: This guide helps toodemonstrate hello deployment of SAP S/4HANA on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="1ea57-163">Biblioteca de dispositivo do SAP na nuvem é um serviço por SAP que permite que aplicações de SAP toodeploy no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-163">SAP Cloud Appliance Library is a service by SAP that allows toodeploy SAP applications on Azure.</span></span> <span data-ttu-id="1ea57-164">Guia de Olá descreve a implementação de Olá passo a passo.</span><span class="sxs-lookup"><span data-stu-id="1ea57-164">hello guide describes step by step hello deployment.</span></span>

<span data-ttu-id="1ea57-165">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-165">Updated: June 2017</span></span>

[<span data-ttu-id="1ea57-166">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-166">This guide can be found here</span></span>](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a><span data-ttu-id="1ea57-167">Elevada disponibilidade de SAP HANA em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-167">High Availability of SAP HANA in Azure Virtual Machines</span></span>
<span data-ttu-id="1ea57-168">Título: aaaHigh disponibilidade de SAP HANA em Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ea57-168">title: aaaHigh Availability of SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="1ea57-169">Resumo: Este guia orienta-o, através da configuração de elevada disponibilidade Olá das Olá SUSE 12 SO e da replicação de sistema HANA tooaccommodate SAP HANA com ativação pós-falha automática.</span><span class="sxs-lookup"><span data-stu-id="1ea57-169">Summary: This guide leads you through hello high availability configuration of hello SUSE 12 OS and SAP HANA tooaccommodate HANA System replication with automatic failover.</span></span> <span data-ttu-id="1ea57-170">Guia de Olá é específico para SUSE e Virtual Machines do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-170">hello guide is specific for SUSE and Azure Virtual Machines.</span></span> <span data-ttu-id="1ea57-171">Guia de Olá aplicável ainda Red Hat ou bare-metal ou privada nuvem ou outras implementações de nuvem pública não do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-171">hello guide does not apply yet for Red Hat or bare-metal or private cloud or other non-Azure public cloud deployments.</span></span>

<span data-ttu-id="1ea57-172">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-172">Updated: June 2017</span></span>

[<span data-ttu-id="1ea57-173">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-173">This guide can be found here</span></span>](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a><span data-ttu-id="1ea57-174">Descrição geral de cópia de segurança SAP HANA em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-174">SAP HANA backup overview on Azure VMs</span></span>
<span data-ttu-id="1ea57-175">Título: aaaBackup guia para SAP HANA em Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ea57-175">title: aaaBackup guide for SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="1ea57-176">Resumo: Este guia fornece informações básicas sobre as possibilidades de cópia de segurança SAP HANA no Azure máquinas virtuais em execução.</span><span class="sxs-lookup"><span data-stu-id="1ea57-176">Summary: This guide provides basic information about backup possibilities running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="1ea57-177">Atualizadas: Março de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-177">Updated: March 2017</span></span>

[<span data-ttu-id="1ea57-178">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-178">This guide can be found here</span></span>](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a><span data-ttu-id="1ea57-179">Backup de nível de ficheiro de SAP HANA em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-179">SAP HANA file level backup on Azure VMs</span></span>
<span data-ttu-id="1ea57-180">Título: cópia de segurança do aaaSAP HANA com base nos instantâneos de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1ea57-180">title: aaaSAP HANA backup based on storage snapshots</span></span>

<span data-ttu-id="1ea57-181">Resumo: Este guia fornece informações sobre como utilizar cópias de segurança baseadas em instantâneos em VMs do Azure ao executar em Azure Virtual Machines de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1ea57-181">Summary: This guide provides information about using snapshot-based backups on Azure VMs when running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="1ea57-182">Atualizadas: Março de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-182">Updated: March 2017</span></span>

[<span data-ttu-id="1ea57-183">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-183">This guide can be found here</span></span>](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a><span data-ttu-id="1ea57-184">Instantâneo de SAP HANA cópias de segurança com base em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-184">SAP HANA snapshot based backups on Azure VMs</span></span>
<span data-ttu-id="1ea57-185">Título: aaaSAP HANA Azure Backup no nível de ficheiro</span><span class="sxs-lookup"><span data-stu-id="1ea57-185">title: aaaSAP HANA Azure Backup on file level</span></span>

<span data-ttu-id="1ea57-186">Resumo: Este guia fornece informações sobre como utilizar o backup de nível de ficheiro de SAP HANA SAP HANA no Azure máquinas virtuais em execução</span><span class="sxs-lookup"><span data-stu-id="1ea57-186">Summary: This guide provides information about using SAP HANA file level backup running SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="1ea57-187">Atualizadas: Março de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-187">Updated: March 2017</span></span>

[<span data-ttu-id="1ea57-188">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-188">This guide can be found here</span></span>](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a><span data-ttu-id="1ea57-189">NetWeaver SAP implementado em Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="1ea57-189">SAP NetWeaver deployed on Azure Virtual Machines</span></span>

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a><span data-ttu-id="1ea57-190">Implementar o sistema SAP IDES no Windows e o SQL Server através de CAL SAP no Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-190">Deploy SAP IDES system on Windows and SQL Server through SAP CAL on Azure</span></span>
<span data-ttu-id="1ea57-191">Título: aaaTesting SAP NetWeaver em VMs do Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="1ea57-191">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="1ea57-192">Resumo: Este documento descreve implementação Olá de um sistema SAP IDES com base no Windows e o SQL Server no Azure utilizando a biblioteca de dispositivo do SAP na nuvem.</span><span class="sxs-lookup"><span data-stu-id="1ea57-192">Summary: This document describes hello deployment of an SAP IDES system based on Windows and SQL Server on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="1ea57-193">Aplicação de nuvem do SAP biblioteca é um serviço SAP que permite que a implementação de Olá dos produtos SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-193">SAP Cloud appliance Library is an SAP service that allows hello deployment of SAP products on Azure.</span></span> <span data-ttu-id="1ea57-194">Este documento vai passo a passo através da implementação de Olá de um sistema SAP IDES.</span><span class="sxs-lookup"><span data-stu-id="1ea57-194">This document goes step by step through hello deployment of an SAP IDES system.</span></span> <span data-ttu-id="1ea57-195">Olá sistema IDES é apenas um exemplo para várias outras dozen aplicações que podem ser implementadas através de aplicação de nuvem de SAP no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-195">hello IDES system is just an example for several other dozen applications that can be deployed through SAP Cloud appliance on Microsoft Azure.</span></span>

<span data-ttu-id="1ea57-196">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-196">Updated: June 2017</span></span>

[<span data-ttu-id="1ea57-197">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-197">This guide can be found here</span></span>](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="1ea57-198">Guia de início rápido para NetWeaver no SUSE Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-198">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="1ea57-199">Título: aaaTesting SAP NetWeaver em VMs do Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="1ea57-199">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="1ea57-200">Resumo: Este artigo descreve vários aspetos tooconsider quando estiver a executar o SAP NetWeaver em máquinas virtuais do Microsoft Azure SUSE Linux (VMs).</span><span class="sxs-lookup"><span data-stu-id="1ea57-200">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="1ea57-201">SAP NetWeaver é oficialmente suportado no SUSE Linux VMs no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-201">SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="1ea57-202">Todos os detalhes sobre as versões de Linux, as versões do SAP kernel e outros detalhes podem ser encontrados na 1928533 de nota SAP "aplicações SAP no Azure: suportada produtos e os tipos VM do Azure".</span><span class="sxs-lookup"><span data-stu-id="1ea57-202">All details regarding Linux versions, SAP kernel versions, and other details can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="1ea57-203">Atualizada: De Setembro de 2016</span><span class="sxs-lookup"><span data-stu-id="1ea57-203">Updated: September 2016</span></span>

[<span data-ttu-id="1ea57-204">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-204">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="1ea57-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planeamento e implementação</span><span class="sxs-lookup"><span data-stu-id="1ea57-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and implementation</span></span>
<span data-ttu-id="1ea57-206">Título: aaaAzure máquinas virtuais de planeamento e implementação de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1ea57-206">title: aaaAzure Virtual Machines planning and implementation for SAP NetWeaver</span></span>

<span data-ttu-id="1ea57-207">Resumo: Este documento é Olá guia toostart com se estiver a pensar sobre como executar SAP NetWeaver em Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="1ea57-207">Summary: This document is hello guide toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="1ea57-208">Este guia de planeamento e implementação ajuda-o a avaliar se um sistema existente ou planeado, com base em SAP NetWeaver pode ser implementado tooan ambiente de Virtual Machines do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-208">This planning and implementation guide helps you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="1ea57-209">Aborda os vários cenários de implementação do SAP NetWeaver e inclui as configurações de SAP que são tooAzure específico.</span><span class="sxs-lookup"><span data-stu-id="1ea57-209">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="1ea57-210">documento de Olá apresenta e descreve todos os Olá necessárias informações de configuração, terá de no Olá SAP/Azure lado toorun uma versão híbrida horizontal SAP.</span><span class="sxs-lookup"><span data-stu-id="1ea57-210">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="1ea57-211">Também são abordadas medidas pode tomar tooensure elevada disponibilidade dos sistemas baseados em SAP NetWeaver no IaaS.</span><span class="sxs-lookup"><span data-stu-id="1ea57-211">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="1ea57-212">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-212">Updated: June 2017</span></span>

<span data-ttu-id="1ea57-213">[Este guia pode ser encontrado aqui][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="1ea57-213">[This guide can be found here][planning-guide]</span></span>

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="1ea57-214">Elevada disponibilidade as configurações do SAP NetWeaver em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-214">High Availability configurations of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="1ea57-215">Título: aaaAzure máquinas virtuais de elevada disponibilidade para SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1ea57-215">title: aaaAzure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="1ea57-216">Resumo: Neste documento, vamos incluem Olá os passos que pode efetuar toodeploy sistemas SAP de elevada disponibilidade no Azure utilizando o modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="1ea57-216">Summary: In this document, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1ea57-217">Vamos guiá-lo estas tarefas principais.</span><span class="sxs-lookup"><span data-stu-id="1ea57-217">We walk you through these major tasks.</span></span> <span data-ttu-id="1ea57-218">Documento Olá, vamos descrever como único-ponto-de-falhas componentes, como o Advanced negócio Application Programming (ABAP) SAP Central serviços (ASCS) / SAP Central serviços (SCS) e sistemas de gestão de base de dados (DBMS) e os componentes redundantes como o SAP Servidor de aplicações que vão toobe protegido quando em execução em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-218">In hello document, we describe how single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server are going toobe protected when running in Azure VMs.</span></span> <span data-ttu-id="1ea57-219">Um exemplo passo a passo de uma instalação e configuração de um sistema SAP de elevada disponibilidade num cluster de Clustering de ativação pós-falha do Windows Server no Azure é demonstrado e apresentado neste documento.</span><span class="sxs-lookup"><span data-stu-id="1ea57-219">A step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure is demonstrated and shown in this document.</span></span>

<span data-ttu-id="1ea57-220">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-220">Updated: June 2017</span></span>

[<span data-ttu-id="1ea57-221">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-221">This guide can be found here</span></span>](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="1ea57-222">Compreender o SID de várias implementações do SAP NetWeaver em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-222">Realizing Multi-SID deployments of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="1ea57-223">Título: aaaCreate uma configuração de várias SID do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1ea57-223">title: aaaCreate an SAP NetWeaver multi-SID configuration</span></span> 

<span data-ttu-id="1ea57-224">Resumo: Este documento é um documento de toohello adição elevada disponibilidade para SAP NetWeaver em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-224">Summary: This document is an addition toohello document High availability for SAP NetWeaver on Azure VMs.</span></span> <span data-ttu-id="1ea57-225">Devido a funcionalidade de toonew no Azure que foi introduzida em Setembro de 2016, é possível toodeploy vários SAP NetWeaver ASCS/SCS instâncias num par de VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-225">Due toonew functionality in Azure that got introduced in September 2016, it is possible toodeploy multiple SAP NetWeaver ASCS/SCS instances in a pair of Azure VMs.</span></span> <span data-ttu-id="1ea57-226">Com a configuração, é possível reduzir o número de Olá das configurações de SAP NetWeaver VMs toodeploy necessário toorealize altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1ea57-226">With such a configuration, you can reduce hello number of VMs necessary toodeploy toorealize highly available SAP NetWeaver configurations.</span></span> <span data-ttu-id="1ea57-227">Guia de Olá descreve a configuração de Olá essas configurações de várias SID.</span><span class="sxs-lookup"><span data-stu-id="1ea57-227">hello guide describes hello setup of such multi-SID configurations.</span></span>

<span data-ttu-id="1ea57-228">Atualizada: De Dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="1ea57-228">Updated: December 2016</span></span>

[<span data-ttu-id="1ea57-229">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-229">This guide can be found here</span></span>](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="1ea57-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Implementação do SAP NetWeaver em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ea57-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="1ea57-231">Título: aaaAzure implementação de máquinas virtuais para SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1ea57-231">title: aaaAzure Virtual Machines deployment for SAP NetWeaver</span></span>

<span data-ttu-id="1ea57-232">Resumo: Este documento fornece orientações sobre o procedimento para implementar SAP NetWeaver software toovirtual máquinas no Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea57-232">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="1ea57-233">Este documento centra-se em três cenários de implementação específicos, com tanta ênfase ao ativar as extensões de monitorização do Olá do Azure para SAP, incluindo as recomendações de Olá extensões de monitorização do Azure para SAP resolução.</span><span class="sxs-lookup"><span data-stu-id="1ea57-233">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="1ea57-234">Este documento parte do princípio de que leu Olá planeamento e guia de implementação.</span><span class="sxs-lookup"><span data-stu-id="1ea57-234">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="1ea57-235">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-235">Updated: June 2017</span></span>

<span data-ttu-id="1ea57-236">[Este guia pode ser encontrado aqui][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="1ea57-236">[This guide can be found here][deployment-guide]</span></span>

### <span data-ttu-id="1ea57-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guia de implementação DBMS</span><span class="sxs-lookup"><span data-stu-id="1ea57-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS deployment guide</span></span>
<span data-ttu-id="1ea57-238">Título: aaaAzure implementação de máquinas virtuais DBMS para SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1ea57-238">title: aaaAzure Virtual Machines DBMS deployment for SAP NetWeaver</span></span>

<span data-ttu-id="1ea57-239">Resumo: Este documento aborda considerações de planeamento e implementação de sistemas DBMS Olá que devem ser executado em conjunto com o SAP.</span><span class="sxs-lookup"><span data-stu-id="1ea57-239">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="1ea57-240">Na primeira parte Olá, as considerações gerais são listadas e apresentadas.</span><span class="sxs-lookup"><span data-stu-id="1ea57-240">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="1ea57-241">Olá seguintes partes documento Olá se relacionam com toodeployments de DBMS diferentes no Azure, que são suportadas pelo SAP.</span><span class="sxs-lookup"><span data-stu-id="1ea57-241">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="1ea57-242">Diferentes DBMS apresentados são do SQL Server, SAP ASE e Oracle.</span><span class="sxs-lookup"><span data-stu-id="1ea57-242">Different DBMS presented are SQL Server, SAP ASE, and Oracle.</span></span> <span data-ttu-id="1ea57-243">Nessas partes específicas, as considerações a ter tooaccount para quando estiver a executar sistemas SAP no Azure em conjunto com essas DBMS são debatidas.</span><span class="sxs-lookup"><span data-stu-id="1ea57-243">In those specific parts, considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="1ea57-244">Assuntos, como os métodos de cópia de segurança e a elevada disponibilidade suportadas pelo Olá que DBMS diferentes no Azure são apresentados para utilização de Olá com aplicações SAP.</span><span class="sxs-lookup"><span data-stu-id="1ea57-244">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="1ea57-245">Atualizadas: Junho de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-245">Updated: June 2017</span></span>

<span data-ttu-id="1ea57-246">[Este guia pode ser encontrado aqui][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1ea57-246">[This guide can be found here][dbms-guide]</span></span>

### <a name="using-azure-site-recovery-for-sap-workload"></a><span data-ttu-id="1ea57-247">Utilizar o Azure Site Recovery para a carga de trabalho do SAP</span><span class="sxs-lookup"><span data-stu-id="1ea57-247">Using Azure Site Recovery for SAP workload</span></span>
<span data-ttu-id="1ea57-248">Título: aaaSAP NetWeaver: criar uma solução de recuperação após desastre com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1ea57-248">title: aaaSAP NetWeaver: Building a Disaster Recovery Solution with Azure Site Recovery</span></span> 

<span data-ttu-id="1ea57-249">Resumo: Este documento descreve a forma de Olá como os serviços do Azure Site Recovery podem ser utilizados para efeitos de Olá de processamento de cenários de recuperação após desastre.</span><span class="sxs-lookup"><span data-stu-id="1ea57-249">Summary: This document describes hello way how Azure Site Recovery services can be used for hello purpose of handling disaster recovery scenarios.</span></span> <span data-ttu-id="1ea57-250">Casos onde Azure é utilizado como localização de recuperação de desastres para um horizontal SAP no local utilizando o Azure Site Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="1ea57-250">Cases where Azure is used as disaster recovery location for an on-premise SAP landscape using Azure Site Recovery Services.</span></span> <span data-ttu-id="1ea57-251">Outro cenário descrito no documento de Olá é o cenário de recuperação de desastre do Olá Azure para o Azure (A2A) e como são gerido com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1ea57-251">Another scenario described in hello document is hello Aure-to-Azure (A2A) disaster recovery case and how it is managed with Azure Site Recovery.</span></span>  

<span data-ttu-id="1ea57-252">Atualizadas: Agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="1ea57-252">Updated: August 2017</span></span>

[<span data-ttu-id="1ea57-253">Este guia pode ser encontrado aqui</span><span class="sxs-lookup"><span data-stu-id="1ea57-253">This guide can be found here</span></span>](http://aka.ms/asr-sap)

