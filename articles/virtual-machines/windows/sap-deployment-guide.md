---
title: "aaaAzure implementação de máquinas virtuais para SAP no Windows | Microsoft Docs"
description: "Saiba como SAP toodeploy software nas máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>Implementar o SAP em VMs do Windows no Azure
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
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
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

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
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
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
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

Máquinas virtuais do Azure é a solução de Olá para organizações que precisam de recursos de computação e armazenamento no tempo mínimo e sem ciclos de aprovisionamento demorado. Pode utilizar máquinas virtuais do Azure toodeploy classical as aplicações, como aplicações baseadas em SAP NetWeaver, no Azure. Expanda uma aplicação a fiabilidade e disponibilidade sem recursos no local adicionais. Máquinas virtuais do Azure suporta uma conectividade entre instalações, pelo que pode integrar Virtual Machines do Azure domínios no local, nuvens privadas e horizontal do sistema SAP da sua organização.

Neste artigo, vamos abordar Olá passos toodeploy SAP as aplicações em máquinas de virtuais (VMs) do Windows no Azure. Este artigo baseia-se nas informações de Olá de [Virtual Machines do Azure de planeamento e implementação de SAP no Windows][planning-guide]. Também complementa a documentação de instalação do SAP e notas de SAP, que são Olá recursos primária para a instalação e implementação de software do SAP.

## <a name="prerequisites"></a>Pré-requisitos
Configurar uma máquina virtual do Azure para a implementação de software do SAP envolve vários passos e recursos. Antes de começar, certifique-se de que cumpre Olá pré-requisitos para instalar o software SAP nas máquinas virtuais do Windows no Azure.

### <a name="local-computer"></a>Computador local
toomanage Windows ou Linux VMs, pode utilizar um script do PowerShell e Olá portal do Azure. Para ambas as ferramentas, precisa de um computador local com o Windows 7 ou uma versão posterior do Windows. Se quiser toomanage só VMs com Linux e pretender que toouse um computador com Linux para esta tarefa, pode utilizar a CLI do Azure.

### <a name="internet-connection"></a>Ligação à Internet
toodownload Olá executar ferramentas e os scripts que são necessárias para a implementação de software do SAP, tem de ser ligado toohello Internet. Olá VM do Azure que está a executar Olá Azure avançada extensão de monitorização para SAP também tem de toohello de acesso à Internet. Se Olá VM do Azure faz parte de uma rede virtual do Azure ou o domínio no local, certifique-se de que estão definidas as definições de proxy relevantes Olá, conforme descrito em [Configurar proxy Olá][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Subscrição do Microsoft Azure
Precisa de uma conta do Azure Active Directory.

### <a name="topology-and-networking"></a>Topologia e de rede
Terá de topologia de Olá toodefine e arquitetura de Olá implementação SAP no Azure:

* Toobe de contas do storage do Azure utilizado
* Rede virtual onde pretende que o sistema do toodeploy Olá SAP
* Toowhich de grupo de recursos que pretende que o sistema do toodeploy Olá SAP
* Região do Azure onde pretende que o sistema do toodeploy Olá SAP
* Configuração de SAP (camada de dois ou três camadas)
* Tamanhos de VM e o número de Olá de discos rígidos virtuais (VHDs) adicionais toobe montado toohello VMs
* Configuração de correção de SAP e sistema de transporte (CTS)

Criar e configurar as contas do storage do Azure e as redes virtuais do Azure antes de começar o processo de implementação de software Olá SAP. Para obter informações sobre como toocreate e configurar estes recursos, consulte [Virtual Machines do Azure de planeamento e implementação de SAP no Windows][planning-guide].

### <a name="sap-sizing"></a>Dimensionamento de SAP
Sabe Olá relativas, dimensionamento do SAP os seguintes:

* Projetado a carga de trabalho do SAP, por exemplo, utilizando a ferramenta de Sizer rápida SAP Olá e número de SAP aplicação desempenho Standard (SAPS) Olá
* Necessário consumo da CPU e recursos de memória do sistema SAP Olá
* Operações necessárias de (e/s) de entrada/saída por segundo
* Necessária largura de banda de rede de comunicação eventual entre VMs no Azure
* Largura de banda de rede necessária entre os recursos no local e Olá sistema SAP implementado o Azure

### <a name="resource-groups"></a>Grupos de recursos
No Gestor de recursos do Azure, pode utilizar toomanage de grupos de recurso todos os recursos da aplicação Olá na sua subscrição do Azure. Para obter mais informações, consulte [descrição geral do Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Recursos

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Recursos SAP
Quando estiver a configurar a implementação de software do SAP, terá de Olá recursos SAP os seguintes:

* A nota [1928533], que tem:
  * Lista de tamanhos de VM do Azure que são suportados para implementação de Olá de software do SAP
  * Informações de capacidade importantes para tamanhos de VM do Azure
  * Software SAP suportado e o sistema operativo (SO) e combinações de base de dados
  * Versão necessária de kernel SAP para o Windows e Linux no Microsoft Azure

* A nota [2015553] apresenta uma lista de pré-requisitos suportado de SAP SAP para implementações de software no Azure.
* A nota [2178632] tem informações detalhadas sobre todas as monitorizações métricas que relatados para SAP no Azure.
* A nota [1409604] Olá requer a versão do agente de anfitrião do SAP para o Windows no Azure.
* A nota [2191498] Olá requer a versão do agente de anfitrião do SAP para Linux no Azure.
* A nota [2243692] tem informações sobre o licenciamento SAP no Linux no Azure.
* A nota [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.
* A nota [2002167] tem informações gerais sobre Red Hat Enterprise Linux 7. x.
* A nota [1999351] tem informações adicionais de resolução de problemas de Olá Azure avançada extensão de monitorização para SAP.
* [WIKI do SAP Comunidade](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as necessárias SAP notas para Linux.
* Cmdlets do PowerShell de SAP específicos que fazem parte do [Azure PowerShell][azure-ps].
* Comandos de CLI do Azure de SAP específicos que fazem parte do [CLI do Azure][azure-cli].

[comment]: <> (Nível de patch MSSedusch TODO adicionar ARM para SAP o agente do anfitrião no 1409604 de nota SAP)

### <a name="microsoft-resources"></a>Recursos da Microsoft
Estes artigos Microsoft abrangem implementações SAP no Azure:

* [Azure máquinas virtuais de planeamento e implementação de SAP no Windows][planning-guide]
* [Implementação de máquinas virtuais do Azure para SAP no Windows (Este artigo)][deployment-guide]
* [Implementação de DBMS de máquinas virtuais do Azure para SAP no Windows][dbms-guide]
* [Portal do Azure][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Cenários de implementação de software SAP em VMs do Azure
Tem várias opções para implementar as VMs e discos associados no Azure. É importante toounderstand Olá diferenças opções de implementação, porque poderá demorar vários passos tooprepare as VMs para implementação com base no tipo de implementação de Olá que escolher.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Cenário 1: Implementar uma VM a partir Olá Azure Marketplace para SAP
Pode utilizar uma imagem fornecida pela Microsoft ou por terceiros em Olá Azure Marketplace toodeploy a VM. Olá Marketplace oferece algumas imagens de SO padrão do Windows Server e diversas distribuições de Linux. Também pode implementar uma imagem que inclui a gestão de base de dados SKUs de sistema (DBMS), por exemplo, o Microsoft SQL Server. Para obter mais informações sobre a utilização de imagens com DBMS SKUs, consulte [implementação DBMS de máquinas virtuais do Azure para SAP no Linux][dbms-guide].

Olá fluxograma a seguir mostra Olá SAP específicos sequência de passos para implementar uma VM do Azure Marketplace de Olá:

![Fluxograma de fase de implementação da VM para sistemas SAP através da utilização de uma imagem de VM de Olá Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Criar uma máquina virtual utilizando Olá portal do Azure
é Olá toocreate da forma mais fácil uma nova máquina virtual com uma imagem de Olá Azure Marketplace utilizando Olá portal do Azure.

1.  Aceda demasiado<https://portal.azure.com/#create>.  Ou, no menu do portal do Azure Olá, selecione **+ novo**.
2.  Selecione **computação**e, em seguida, selecione o tipo de Olá de que pretende toodeploy o sistema operativo. Por exemplo, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) ou Red Hat Enterprise Linux 7.2 (RHEL 7.2). Vista de lista predefinida de Olá não mostra que todos os sistemas operativos suportados. Selecione **ver todos os** para uma lista completa. Para mais informações sobre sistemas operativos suportados para a implementação de software do SAP, consulte a nota SAP [1928533].
3.  Na página seguinte do Olá, reveja os termos e condições.
4.  No Olá **selecionar um modelo de implementação** caixa, selecione **Resource Manager**.
5.  Selecione **Criar**.

Assistente de Olá orienta-o a definição de máquina de virtual Olá necessário parâmetros toocreate Olá, além disso tooall necessários recursos, como as contas de armazenamento e de interfaces de rede. Algumas destes parâmetros são:

1. **Noções básicas**:
  * **Nome**: nome de Olá do recurso de Olá (nome da máquina virtual Olá).
 * **Nome de utilizador e palavra-passe** ou **chave pública SSH**: introduza Olá nome de utilizador e palavra-passe do utilizador Olá que é criado durante o aprovisionamento de Olá. Para uma máquina virtual do Linux, pode introduzir chave Secure Shell (SSH) pública Olá que utilize toosign toohello máquina.
 * **Subscrição**: selecione a subscrição Olá que pretende que o toouse tooprovision Olá nova máquina virtual.
 * **Grupo de recursos**: nome de Olá Olá do grupo de recursos para Olá VM. Pode introduzir um nome de Olá de um novo grupo ou Olá nome de recurso de um grupo de recursos que já existe.
 * **Localização**: onde toodeploy Olá nova máquina virtual. Se pretender que a rede do tooconnect Olá máquina virtual tooyour no local, certifique-se de que selecionar Olá localização de rede virtual Olá que estabelece ligação de rede no local de tooyour do Azure. Para obter mais informações, consulte [redes do Microsoft Azure] [ planning-guide-microsoft-azure-networking] no [Virtual Machines do Azure de planeamento e implementação de SAP no Linux] [ planning-guide].
2. **Tamanho**:

     Para obter uma lista de tipos VM suportados, consulte a nota SAP [1928533]. Lembre-se de que selecionar o tipo VM correto Olá se quiser toouse Premium Storage do Azure. Nem todos os tipos VM suportam o Premium Storage. Para obter mais informações, consulte [Storage: armazenamento do Microsoft Azure e discos de dados] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] e [Premium Storage do Azure] [ planning-guide-azure-premium-storage] no [ Azure máquinas virtuais de planeamento e implementação de SAP no Linux][planning-guide].

3. **Definições**:
   * **Conta de armazenamento**: selecione uma conta de armazenamento existente ou crie um novo. Nem todos os tipos de armazenamento funcionam para executar aplicações SAP. Para obter mais informações sobre os tipos de armazenamento, consulte [armazenamento do Microsoft Azure] [ dbms-guide-2.3] no [implementação DBMS de máquinas virtuais do Azure para SAP no Linux] [ dbms-guide].
   * **Rede virtual** e **sub-rede**: toointegrate Olá máquina de virtual com a sua intranet, selecione Olá de rede virtual é a rede no local de tooyour ligado.
   * **Endereço IP público**: selecione Olá endereço IP público que pretende toouse, ou introduza parâmetros toocreate um novo endereço IP público. Pode utilizar um tooaccess de endereço IP público a máquina virtual através de Olá Internet. Certifique-se que crie também uma segurança rede grupo toohelp acesso seguro tooyour da máquina virtual.
   * **Grupo de segurança de rede**: para obter mais informações, consulte [controlar o fluxo de tráfego de rede com grupos de segurança de rede][virtual-networks-nsg].
   * **Disponibilidade**: selecione um conjunto de disponibilidade, ou introduza Olá parâmetros toocreate uma disponibilidade novo conjunto. Para obter mais informações, consulte [conjuntos de disponibilidade do Azure][planning-guide-3.2.3].
   * **Monitorização**: pode selecionar **desativar** para monitorização do diagnóstico. Este é ativado automaticamente ao executar Olá comandos tooenable Olá Azure avançada extensão de monitorização, conforme descrito em [configurar monitorização][deployment-guide-configure-monitoring-scenario-1].

4. **Resumo**:

  Reveja as suas seleções e, em seguida, selecione **OK**.

A máquina virtual é implementada no grupo de recursos de Olá que selecionou.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Criar uma máquina virtual utilizando um modelo
Pode criar uma máquina virtual utilizando um dos modelos SAP Olá publicados no Olá [repositório do GitHub modelos do início rápido do azure][azure-quickstart-templates-github]. Também pode criar manualmente uma máquina virtual utilizando Olá [portal do Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], ou [CLI do Azure ][virtual-machines-linux-tutorial].

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap-2-camada--imagem do marketplace)][sap-templates-2-tier-marketplace-image]

  toocreate um sistema de duas camadas utilizando apenas uma máquina virtual, utilizar este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais)** (sap-3-camada--imagem do marketplace)][sap-templates-3-tier-marketplace-image]

  toocreate um sistema de três camadas utilizando várias máquinas virtuais, utilizar este modelo.

No portal do Azure Olá, introduza Olá seguir os parâmetros para o modelo de Olá:

1. **Noções básicas**:
  * **Subscrição**: modelo de Olá Olá subscrição toouse toodeploy.
  * **Grupo de recursos**: modelo Olá de toodeploy toouse Olá recursos grupo. Pode criar um novo grupo de recursos ou pode selecionar um grupo de recursos existente na subscrição Olá.
  * **Localização**: onde toodeploy Olá modelo. Se tiver selecionado um grupo de recursos existente, a localização de Olá desse grupo de recursos é utilizada.

2. **Definições**:
  * **ID de sistema do SAP**: Olá SAP sistema ID (SID).
  * **Tipo de SO**: Olá o sistema operativo que pretende toodeploy, por exemplo, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) ou Red Hat Enterprise Linux 7.2 (RHEL 7.2).

    Vista de lista predefinida de Olá não mostra que todos os sistemas operativos suportados. Selecione **ver todos os** para uma lista completa. Para mais informações sobre sistemas operativos suportados para a implementação de software do SAP, consulte a nota SAP [1928533].
  * **Tamanho do sistema SAP**: Olá tamanho de Olá sistema SAP.

    número de Olá de novo sistema do SAPS Olá fornece. Se tiver a não certeza necessita de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.
  * **Disponibilidade do sistema** (apenas modelo de três camadas): Olá disponibilidade do sistema.

    Selecione **HA** para uma configuração que é adequada para uma instalação de elevada disponibilidade. São criados dois servidores de base de dados e dois servidores para ABAP SAP Central serviços (ASCS).
  * **Tipo de armazenamento** (apenas modelo de duas camadas): tipo de armazenamento toouse de Olá.

    Para sistemas maiores, recomendamos vivamente a utilizar o Premium Storage do Azure. Para obter mais informações sobre os tipos de armazenamento, consulte estes recursos:
      * [Utilização do armazenamento SSD Premium do Azure para a instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure] [ dbms-guide-2.3] no [implementação DBMS de máquinas virtuais do Azure para SAP no Linux][dbms-guide]
      * [Armazenamento Premium: Armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft Storage do Azure][storage-introduction]
  * **Nome de utilizador de Admin** e **palavra-passe de administrador**: um nome de utilizador e palavra-passe.
    É criado um novo utilizador, para iniciar sessão na máquina virtual de toohello.
  * **Novo ou existente sub-rede**: determina se são criados um nova rede virtual e uma sub-rede ou se é utilizada uma sub-rede existente. Se já tiver uma rede virtual que é a rede no local de tooyour ligado, selecione **existentes**.
  * **ID de sub-rede**: Olá ID de sub-rede de Olá Olá máquinas de virtuais serão ligados. Selecione a sub-rede de Olá da sua rede privada virtual (VPN) ou Azure ExpressRoute rede virtual toouse tooconnect Olá máquina virtual tooyour rede no local. ID de Olá, normalmente, este aspeto: /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}&lt;id de subscrição > /resourceGroups/&lt;nome do grupo de recursos > /providers/Microsoft.Network/virtualNetworks/&lt;nome da rede virtual > /subnets/&lt;nome de sub-rede >

3. **Termos e condições**:  
    Reveja e aceite os termos legais Olá.

4.  Selecione **Compra**.

Olá agente da VM do Azure é implementado por predefinição, quando utiliza uma imagem de Olá Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Configurar definições de proxy
Dependendo de como a sua rede no local é configurado, poderá ser necessário tooset segurança proxy Olá na VM. Se a VM estiver a rede no local de tooyour ligado através de VPN ou ExpressRoute, Olá VM poderá não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou recolher dados de monitorização. Para obter mais informações, consulte [Configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Aderir a um domínio (apenas Windows)
Se a implementação do Azure tooan ligado no local do Active Directory ou o DNS instância através de uma ligação de VPN de site para site Azure ou ExpressRoute (esta opção é denominada *em vários locais* no [planeamento de Virtual Machines do Azure e implementação de SAP no Linux][planning-guide]), é esperado que Olá VM é efetuar a adesão um domínio no local. Para obter mais informações sobre as considerações para esta tarefa, consulte [aderir a um domínio no local tooan VM (apenas Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configurar a monitorização
Se o seu ambiente suportar SAP, configurar Olá extensão de monitorização do Azure para SAP, conforme descrito em toobe [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5]. A verificação dos pré-requisitos de Olá para SAP monitorização e mínimo as versões necessárias do SAP Kernel e o agente de anfitrião do SAP, recursos de Olá listado no [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitorização
Verificar se monitorização está a funcionar, conforme descrito em [verificações e a resolução de problemas para configurar a monitorização ponto-a-ponto][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Passos de pós-implementação
Depois de criar Olá VM e Olá VM é implementado, tem de componentes de software tooinstall Olá necessário no Olá VM. Devido a sequência de instalação do software/implementação Olá neste tipo de implementação da VM, Olá software toobe instalado já deve estar disponível no Azure, na outra VM, ou como um disco que pode ser anexado. Em alternativa, considere utilizar um cenário de vários locais, na qual conectividade toohello no local ativos (partilhas de instalação) é fornecido.

Depois de implementar a VM no Azure, siga Olá mesmo diretrizes e as ferramentas tooinstall Olá SAP software na sua VM como teria num ambiente no local. software SAP tooinstall numa VM do Azure, ambos SAP e a Microsoft recomenda que carregar e armazena o suporte de dados de instalação de SAP de Olá em VHDs do Azure ou a criação de uma VM do Azure que funciona como um servidor de ficheiros que tenha todos os Olá necessário suporte de dados de instalação de SAP.

[comment]: <> (TAREFAS de MSSedusch por que motivo é necessário toorecommend um gestão de ficheiros, por exemplo, servidor de ficheiros ou VHD? É que, por isso, diferente no local?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Cenário 2: Implementar uma VM com uma imagem personalizada para SAP
Porque diferentes versões de um sistema operativo ou o DBMS tem requisitos diferentes patch, imagens de Olá que encontrará no Olá Azure Marketplace poderão não satisfazer as suas necessidades. Em vez disso, poderá toocreate uma VM utilizando a sua própria imagem de SO/DBMS VM, que pode implementar novamente mais tarde.
Utilize diferentes passos toocreate uma imagem privada para Linux ao toocreate um para o Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare uma imagem do Windows que pode utilizar toodeploy várias máquinas virtuais, definições do Windows hello (como o SID do Windows e o nome de anfitrião) tem de ser abstracted ou generalizado no Olá VM no local. Pode utilizar [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo isto.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare uma imagem de Linux que pode ser utilizado toodeploy várias máquinas virtuais, algumas definições de Linux tem de ser Olá abstracted ou generalizado no local VM. Pode utilizar `waagent -deprovision` toodo isto. Para obter mais informações, consulte [capturar uma máquina virtual do Linux em execução no Azure] [ virtual-machines-linux-capture-image] e Olá [guia de utilizador do agente Linux do Azure][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Preparar e criar uma imagem personalizada e, em seguida, utilizá-lo toocreate várias VMs novas. Isto é descrito no [Virtual Machines do Azure de planeamento e implementação de SAP no Linux][planning-guide]. Configurar a base de dados de conteúdo utilizando o Gestor de aprovisionamento de Software para SAP tooinstall um novo sistema SAP (restaura uma cópia de segurança da base de dados a partir de um VHD que está a máquina virtual de toohello ligado) ou por diretamente a restaurar uma cópia de segurança da base de dados do storage do Azure, se o DBMS o suportar. Para obter mais informações, consulte [implementação DBMS de máquinas virtuais do Azure para SAP no Linux][dbms-guide]. Se já tiver instalado um sistema SAP na sua VM no local (especialmente para sistemas de duas camadas), pode adaptar as definições do sistema SAP Olá após a implementação de Olá de Olá VM do Azure, utilizando os procedimento de mudar o nome do sistema de Olá suportado pelo aprovisionamento de Software do SAP Gestor (nota SAP [1619720]). Caso contrário, pode instalar software SAP Olá depois de implementar Olá VM do Azure.

Olá fluxograma a seguir mostra Olá SAP específicos sequência de passos para implementar uma VM a partir de uma imagem personalizada:

![Fluxograma de fase de implementação da VM para sistemas SAP através da utilização de uma imagem de VM no Marketplace privada][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Criar máquina virtual de Olá
toocreate uma implementação através da utilização de uma imagem do SO privada de Olá portal do Azure, utilize um dos Olá seguintes modelos SAP. Estes modelos são publicados no Olá [repositório do GitHub modelos do início rápido do azure][azure-quickstart-templates-github]. Também pode criar manualmente uma máquina virtual, utilizando [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap-2-camada-utilizador-imagem)][sap-templates-2-tier-user-image]

  toocreate um sistema de duas camadas utilizando apenas uma máquina virtual, utilizar este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais)** (sap-3-camada-utilizador-imagem)][sap-templates-3-tier-user-image]

  toocreate um sistema de três camadas com várias máquinas virtuais ou a seus próprios imagem do SO, utilizar este modelo.

No portal do Azure Olá, introduza Olá seguir os parâmetros para o modelo de Olá:

1. **Noções básicas**:
  * **Subscrição**: modelo de Olá Olá subscrição toouse toodeploy.
  * **Grupo de recursos**: modelo Olá de toodeploy toouse Olá recursos grupo. Pode criar um novo grupo de recursos ou selecione um grupo de recursos existente na subscrição Olá.
  * **Localização**: onde toodeploy Olá modelo. Se tiver selecionado um grupo de recursos existente, a localização de Olá desse grupo de recursos é utilizada.
2. **Definições**:
  * **ID de sistema do SAP**: Olá ID do sistema de SAP.
  * **Tipo de SO**: Olá o tipo de sistema operativo que pretende toodeploy (Windows ou Linux).
  * **Tamanho do sistema SAP**: Olá tamanho de Olá sistema SAP.

    número de Olá de novo sistema do SAPS Olá fornece. Se tiver a não certeza necessita de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.
  * **Disponibilidade do sistema** (apenas modelo de três camadas): Olá disponibilidade do sistema.

    Selecione **HA** para uma configuração que é adequada para uma instalação de elevada disponibilidade. São criados dois servidores de base de dados e dois servidores para ASCS.
  * **Tipo de armazenamento** (apenas modelo de duas camadas): tipo de armazenamento toouse de Olá.

    Para sistemas maiores, recomendamos vivamente a utilizar o Premium Storage do Azure. Para obter mais informações sobre os tipos de armazenamento, consulte Olá os seguintes recursos:
      * [Utilização do armazenamento SSD Premium do Azure para a instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure] [ dbms-guide-2.3] no [implementação DBMS de máquinas virtuais do Azure para SAP no Linux][dbms-guide]
      * [Armazenamento Premium: Armazenamento de elevado desempenho para cargas de trabalho de máquina virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft Storage do Azure][storage-introduction]
  * **Imagem do utilizador URI de VHD**: Olá URI Olá privada da imagem do SO VHD, por exemplo, https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Conta de armazenamento de imagem de utilizador**: nome de Olá Olá da conta de armazenamento onde está armazenada a imagem do SO privada Olá, por exemplo, &lt;accountname > no https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Nome de utilizador de Admin** e **palavra-passe de administrador**: Olá nome de utilizador e palavra-passe.

    É criado um novo utilizador, para iniciar sessão na máquina virtual de toohello.
  * **Novo ou existente sub-rede**: determina se é criada uma nova rede virtual e uma sub-rede ou se é utilizada uma sub-rede existente. Se já tiver uma rede virtual que é a rede no local de tooyour ligado, selecione **existentes**.
  * **ID de sub-rede**: Olá ID Olá sub-rede toowhich Olá máquinas virtuais serão ligados. Selecione Olá sub-rede da sua VPN ou ExpressRoute rede virtual toouse tooconnect Olá máquina virtual tooyour na rede local. ID de Olá, normalmente, este aspeto:

    /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}&lt;id de subscrição > /resourceGroups/&lt;nome do grupo de recursos > /providers/Microsoft.Network/virtualNetworks/&lt;nome da rede virtual > /subnets/&lt;nome de sub-rede >

3. **Termos e condições**:  
    Reveja e aceite os termos legais Olá.

4.  Selecione **Compra**.

#### <a name="install-hello-vm-agent-linux-only"></a>Instalar Olá agente da VM (apenas Linux)
modelos de Olá toouse descritos Olá anterior a secção, Olá que agente Linux tem de estar instalado na imagem do utilizador Olá ou Olá implementação irá falhar. Transfira e instale Olá agente da VM na imagem do utilizador Olá, conforme descrito em [transferir, instalar e ativar Olá agente da VM do Azure][deployment-guide-4.4]. Se não utilizar modelos de Olá, também pode instalar o agente da VM de Olá mais tarde.

#### <a name="join-a-domain-windows-only"></a>Aderir a um domínio (apenas Windows)
Se a implementação do Azure tooan ligado no local do Active Directory ou o DNS instância através de uma ligação de VPN de site para site Azure ou Azure ExpressRoute (esta opção é denominada *em vários locais* no [Virtual Machines do Azure planeamento e implementação de SAP no Linux][planning-guide]), é esperado que Olá VM é efetuar a adesão um domínio no local. Para obter mais informações sobre as considerações para este passo, consulte [aderir a um domínio no local tooan VM (apenas Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configurar definições de proxy
Dependendo de como a sua rede no local é configurado, poderá ser necessário tooset segurança proxy Olá na VM. Se a VM estiver a rede no local de tooyour ligado através de VPN ou ExpressRoute, Olá VM poderá não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou recolher dados de monitorização. Para obter mais informações, consulte [Configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurar a monitorização
Se o seu ambiente suportar SAP, configurar Olá extensão de monitorização do Azure para SAP, conforme descrito em toobe [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5]. A verificação dos pré-requisitos de Olá para SAP monitorização e mínimo as versões necessárias do SAP Kernel e o agente de anfitrião do SAP, recursos de Olá listado no [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitorização
Verificar se monitorização está a funcionar, conforme descrito em [verificações e a resolução de problemas para configurar a monitorização ponto-a-ponto][deployment-guide-troubleshooting-chapter].




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Cenário 3: Mover uma VM no local através da utilização de um VHD de Azure não generalizado com o SAP
Neste cenário, deve planear toomove sistema SAP específico de uma tooAzure de ambiente no local. Pode fazê-lo através do carregamento Olá VHD que tenha Olá SO, binários SAP Olá, e, eventualmente, Olá binários DBMS plus VHDs Olá com dados Olá e ficheiros de Olá DBMS, tooAzure de registo. Ao contrário do cenário de Olá descrito [cenário 2: implementar uma VM com uma imagem personalizada para SAP][deployment-guide-3.3], neste caso, mantenha o nome de anfitrião do Olá, SAP SID, e as contas de utilizador SAP no Olá VM do Azure, porque estavam configurado no ambiente do Olá no local. Não é necessário toogeneralize Olá SO. Este cenário aplica-se com mais frequência cenários toocross local onde parte Olá horizontal SAP é executado no local e parte do mesmo é executado no Azure.

Neste cenário, Olá agente da VM não é automaticamente instalado durante a implementação. Porque Olá agente da VM e Olá Azure avançada extensão de monitorização para SAP necessários para toorun SAP, terá de toodownload, instalar e ativar os dois componentes manualmente depois de criar a máquina virtual de Olá.

Para obter mais informações sobre Olá agente da VM do Azure, consulte Olá os seguintes recursos.

[comment]: <> (Ligação de Windows de atualização de MSSedusch TODO abaixo)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/Archive/2014/02/17/bginfo-Guest-Agent-Extension-for-Azure-VMS.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Guia de utilizador do agente Linux do Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Olá fluxograma a seguir mostra a sequência de Olá dos passos para mover uma VM no local através da utilização de um VHD de Azure não generalizado:

![Fluxograma de fase de implementação da VM para sistemas SAP através da utilização de um disco VM][deployment-guide-figure-400]

Partindo do princípio que hello disco é já carregado e definido no Azure (consulte [Virtual Machines do Azure de planeamento e implementação de SAP no Linux][planning-guide]), efetue Olá tarefas descritas nos Olá junto secções alguns.

#### <a name="create-a-virtual-machine"></a>Criar uma máquina virtual
toocreate uma implementação através da utilização de um disco de SO privado através de Olá portal do Azure, utilize o modelo SAP de Olá publicado no Olá [repositório do GitHub modelos do início rápido do azure][azure-quickstart-templates-github]. Também pode criar manualmente uma máquina virtual, utilizando o PowerShell.

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap 2-camada-utilizador-disco)][sap-templates-2-tier-os-disk]

  toocreate um sistema de duas camadas utilizando apenas uma máquina virtual, utilizar este modelo.

No portal do Azure Olá, introduza Olá seguir os parâmetros para o modelo de Olá:

1. **Noções básicas**:
  * **Subscrição**: modelo de Olá Olá subscrição toouse toodeploy.
  * **Grupo de recursos**: modelo Olá de toodeploy toouse Olá recursos grupo. Pode criar um novo grupo de recursos ou selecione um grupo de recursos existente na subscrição Olá.
  * **Localização**: onde toodeploy Olá modelo. Se tiver selecionado um grupo de recursos existente, a localização de Olá desse grupo de recursos é utilizada.
2. **Definições**:
  * **ID de sistema do SAP**: Olá ID do sistema de SAP.
  * **Tipo de SO**: Olá o tipo de sistema operativo que pretende toodeploy (Windows ou Linux).
  * **Tamanho do sistema SAP**: Olá tamanho de Olá sistema SAP.

    número de Olá de novo sistema do SAPS Olá fornece. Se tiver a não certeza necessita de sistema de Olá SAPS quantos, peça ao seu parceiro de tecnologia de SAP ou integrador de sistema.
  * **Tipo de armazenamento** (apenas modelo de duas camadas): tipo de armazenamento toouse de Olá.

    Para sistemas maiores, recomendamos vivamente a utilizar o Premium Storage do Azure. Para obter mais informações sobre os tipos de armazenamento, consulte Olá os seguintes recursos:
      * [Utilização do armazenamento SSD Premium do Azure para a instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure] [ dbms-guide-2.3] no [implementação DBMS de Máquina Virtual do Azure para SAP no Linux][dbms-guide]
      * [Armazenamento Premium: Armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft Storage do Azure][storage-introduction]
  * **URI do VHD do disco de SO**: Olá URI de disco de SO privado Olá, por exemplo, https://&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Novo ou existente sub-rede**: determina se são criados um nova rede virtual e uma sub-rede ou se é utilizada uma sub-rede existente. Se já tiver uma rede virtual que é a rede no local de tooyour ligado, selecione **existentes**.
  * **ID de sub-rede**: Olá ID Olá sub-rede toowhich Olá máquinas virtuais serão ligados. Selecione Olá sub-rede da sua VPN ou Azure ExpressRoute rede virtual toouse tooconnect Olá máquina virtual tooyour na rede local. ID de Olá, normalmente, este aspeto:

    /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname}&lt;id de subscrição > /resourceGroups/&lt;nome do grupo de recursos > /providers/Microsoft.Network/virtualNetworks/&lt;nome da rede virtual > /subnets/&lt;nome de sub-rede >

3. **Termos e condições**:  
    Reveja e aceite os termos legais Olá.

4.  Selecione **Compra**.

#### <a name="install-hello-vm-agent"></a>Instalar Olá agente da VM
Olá, Olá toouse modelos são descritos na secção anterior, hello agente da VM tem de estar instalado no disco Olá SO ou Olá implementação irá falhar. Transfira e instale Olá agente da VM no Olá VM, conforme descrito em [transferir, instalar e ativar Olá agente da VM do Azure][deployment-guide-4.4].

Se não utilizar modelos de Olá descritos Olá anterior a secção, também pode instalar o agente da VM de Olá posteriormente.

#### <a name="join-a-domain-windows-only"></a>Aderir a um domínio (apenas Windows)
Se a implementação do Azure tooan ligado no local do Active Directory ou o DNS instância através de uma ligação de VPN de site para site Azure ou ExpressRoute (esta opção é denominada *em vários locais* no [planeamento de Virtual Machines do Azure e implementação de SAP no Linux][planning-guide]), é esperado que Olá VM é efetuar a adesão um domínio no local. Para obter mais informações sobre as considerações para esta tarefa, consulte [aderir a um domínio no local tooan VM (apenas Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Configurar definições de proxy
Dependendo de como a sua rede no local é configurado, poderá ser necessário tooset segurança proxy Olá na VM. Se a VM estiver a rede no local de tooyour ligado através de VPN ou ExpressRoute, Olá VM poderá não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou recolher dados de monitorização. Para obter mais informações, consulte [Configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurar a monitorização
Se o seu ambiente suportar SAP, configurar Olá extensão de monitorização do Azure para SAP, conforme descrito em toobe [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5]. A verificação dos pré-requisitos de Olá para SAP monitorização e mínimo as versões necessárias do SAP Kernel e o agente de anfitrião do SAP, recursos de Olá listado no [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitorização
Verificar se monitorização está a funcionar, conforme descrito em [verificações e a resolução de problemas para configurar a monitorização ponto-a-ponto][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Atualizar a configuração de monitorização de Olá para SAP
Atualize a configuração de monitorização SAP Olá em qualquer um dos seguintes cenários de Olá:
* equipa de Microsoft/SAP conjunta Olá expande Olá capacidades de monitorização e os pedidos de contadores mais ou menos.
* Microsoft disponibiliza uma nova versão do Olá subjacente infraestrutura do Azure que fornece dados de monitorização de Olá e Olá extensão de monitorização avançada da Azure para SAP necessidades toobe adaptada descritos toothose alterações.
* Montar adicional VHDs tooyour VM do Azure ou remover um VHD. Neste cenário, atualize a coleção de Olá de dados relacionados com o armazenamento. Alterar a configuração, adicionando ou eliminando pontos finais ou através da atribuição de IP endereços tooa VM não afeta a configuração de monitorização de Olá.
* Alterar tamanho Olá da sua VM do Azure, por exemplo, do tamanho A5 tooany outro tamanho da VM.
* Adicionar novo tooyour de interfaces de rede VM do Azure.

tooupdate monitorização definições, Olá atualização monitorizar a infraestrutura por Olá seguir os passos em [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Tarefas detalhadas de implementação de software do SAP numa VM do Windows
Esta secção descreve em pormenor os passos para efetuar tarefas específicas no processo de configuração e implementação de Olá.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Implementar os cmdlets do PowerShell do Azure
1.  Aceda demasiado[transfere do Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Em **ferramentas da linha de comandos**, em **PowerShell**, selecione **Windows instalar**.
3.  Na caixa de diálogo Gestor de transferência da Microsoft hello, para o ficheiro de Olá transferido (por exemplo, WindowsAzurePowershellGet.3f.3f.3fnew.exe), selecione **executar**.
4.  toorun instalador de plataforma Web da Microsoft (Microsoft instalador de plataforma Web), selecione **Sim**.
5.  Uma página que parece que este é apresentado:

  ![Página de instalação para os cmdlets do PowerShell do Azure][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecione **instalar**e, em seguida, aceitar termos de licenciamento de Software do Olá Microsoft.
7.  O PowerShell está instalado. Selecione **concluir** Assistente de instalação de Olá tooclose.

Verifique frequentemente para atualizações toohello os cmdlets do PowerShell, que normalmente são atualizados mensalmente. Olá toocheck de forma mais fácil para atualizações é Olá toodo precedente passos de instalação, página de instalação de toohello mostrado no passo 5. Olá data e a versão do número de versão dos cmdlets de Olá está incluído na página Olá mostrada no passo 5. Salvo indicação em contrário no nota SAP [1928533] ou nota SAP [2015553], recomendamos que trabalhe com a versão mais recente do Olá de cmdlets do PowerShell do Azure.

versão de Olá toocheck do Olá cmdlets Azure PowerShell que são instalados no seu computador, execute este comando do PowerShell:
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
resultado de Olá tem o seguinte aspeto:

![Resultado da verificação da versão do cmdlet do PowerShell do Azure][deployment-guide-figure-600]
<a name="figure-6"></a>

Se a versão de cmdlet do Azure Olá instalado no seu computador é uma versão atual Olá, primeira página de Olá do Assistente de instalação de Olá indica que adicionando **(instalada)** título do produto toohello (consulte Olá seguinte captura de ecrã). Os cmdlets do PowerShell Azure estão atualizados. tooclose Olá Assistente de instalação, selecione **saída**.

![Página de instalação para os cmdlets do Azure PowerShell com a indicação de que Olá mais recente a versão de cmdlets do PowerShell do Azure estão instalados][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Implementar a CLI do Azure
1.  Aceda demasiado[transfere do Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Em **ferramentas da linha de comandos**, em **interface de linha de comandos do Azure**, selecione Olá **instalar** ligação para o seu sistema operativo.
3.  Na caixa de diálogo Gestor de transferência da Microsoft hello, para o ficheiro de Olá transferido (por exemplo, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), selecione **executar**.
4.  toorun instalador de plataforma Web da Microsoft (Microsoft instalador de plataforma Web), selecione **Sim**.
5.  Uma página que parece que este é apresentado:

  ![Página de instalação para os cmdlets do PowerShell do Azure][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecione **instalar**e, em seguida, aceitar termos de licenciamento de Software do Olá Microsoft.
7.  CLI do Azure está instalado. Selecione **concluir** Assistente de instalação de Olá tooclose.

Verifique frequentemente para atualizações tooAzure CLI, que normalmente é atualizada mensalmente. Olá toocheck de forma mais fácil para atualizações é Olá toodo precedente passos de instalação, página de instalação de toohello mostrado no passo 5.


versão de Olá toocheck da CLI do Azure que está instalado no seu computador, execute este comando:
```
azure --version
```

resultado de Olá tem o seguinte aspeto:

![Resultado da verificação da versão do CLI do Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Aderir a um domínio no local tooan VM (apenas Windows)
Se implementar SAP VMs num cenário em vários locais, onde são expandidas do Active Directory no local e o DNS no Azure, é esperado que Olá VMs são associação a um domínio no local. Olá, os passos detalhados que tomar toojoin domínio VM tooan no local, e hello software adicional necessário toobe um membro de um domínio no local, varia pelo cliente. Normalmente, toojoin tooan uma VM no local domínio, tem de tooinstall software adicional, como o antimalware software e o software de cópia de segurança ou de monitorização.

Neste cenário, terá também toomake certificar-se de que se as definições de proxy da Internet são forçadas quando uma VM associado um domínio no seu ambiente, o Windows hello, tem de conta do sistema Local (S-1-5-18) na VM do convidado de Olá Olá mesmas definições de proxy. opção mais fácil Olá tem o proxy de Olá tooforce utilizando um política de grupo, o que se aplica toosystems no domínio Olá de domínio.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Transferir, instalar e ativar Olá agente da VM do Azure
Para máquinas virtuais que sejam implementadas a partir de uma imagem do SO que não seja generalizada (por exemplo, uma imagem que não têm origem na ferramenta de preparação de sistema do Windows ou o sysprep, Olá), terá de toomanually transferir, instalar e ativar Olá agente da VM do Azure.

Se implementar uma VM a partir Olá Azure Marketplace, este passo não é necessário. Imagens de Olá Azure Marketplace já tem Olá agente da VM do Azure.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Transferir Olá agente da VM do Azure:
  1.  Transferir Olá [pacote instalador do agente da VM do Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Armazenar o pacote MSI do agente de VM é Olá localmente num servidor ou computador pessoal.
2.  Instale Olá agente da VM do Azure:
  1.  Ligar toohello implementado VM do Azure utilizando o protocolo RDP (Remote Desktop Protocol).
  2.  Abra uma janela do Explorador do Windows hello VM e o diretório de destino selecione Olá do ficheiro MSI Olá do Olá agente da VM.
  3.  Arraste Olá MSI de instalador do agente de VM do Azure ficheiro a partir do seu diretório de destino do computador local/servidor toohello de Olá agente da VM no Olá VM.
  4.  Faça duplo clique em ficheiro MSI Olá Olá VM.
3.  Para VMs que são domínios local tooon associados, certifique-se de que as definições de proxy de Internet eventual também se aplicam toohello conta de sistema Local do Windows (S-1-5-18) no Olá VM, conforme descrito em [Configurar proxy Olá] [ deployment-guide-configure-proxy]. Olá agente da VM é executado neste contexto e tem de toobe tooconnect capaz de tooAzure.

Sem interação do utilizador é necessário tooupdate Olá agente da VM do Azure. Olá agente da VM é atualizada automaticamente e não requer um reinício VM.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Utilize Olá os seguintes comandos tooinstall Olá agente da VM para Linux:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

Se já estiver instalado o agente de Olá, tooupdate Olá agente Linux do Azure, Olá passos descritos no [Olá de atualização agente Linux do Azure numa VM toohello mais recente versão do GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configurar o proxy de Olá
passos de Olá que tirar o proxy de Olá tooconfigure do Windows são diferentes de forma Olá que configurar proxy Olá no Linux.

#### <a name="windows"></a>Windows
As definições de proxy devem ser definidas corretamente para Olá tooaccess Olá Internet de conta de sistema Local. Se as definições de proxy não estão definidas pela política de grupo, pode configurar as definições de Olá para Olá conta do sistema Local.

1. Aceda demasiado**iniciar**, introduza **gpedit.msc**e, em seguida, selecione **Enter**.
2. Selecione **configuração do computador** > **modelos administrativos** > **componentes do Windows** > **do Internet Explorer**. Certifique-se de que essa definição Olá **tornar proxy definições por computador (em vez de por utilizador)** está desativada ou não está configurado.
3. No **painel de controlo**, aceda demasiado**Centro de partilha de rede e** > **opções da Internet**.
4. No Olá **ligações** separador, selecione de Olá **definições de LAN** botão.
5. Limpar Olá **detetar automaticamente as definições** caixa de verificação.
6. Selecione Olá **utilizar um servidor proxy para a sua LAN** caixa de verificação e, em seguida, introduza o endereço de proxy de Olá e a porta.
7. Selecione Olá **avançadas** botão.
8. No Olá **exceções** box, introduza o endereço IP Olá **168.63.129.16**. Selecione **OK**.


#### <a name="linux"></a>Linux
Configurar o proxy correta Olá no ficheiro de configuração de Olá de Olá agente de convidado do Microsoft Azure, que está localizado em \\etc\\waagent.conf.

Definir Olá os seguintes parâmetros:

1.  **Anfitrião de proxy HTTP**. Por exemplo, defina demasiado**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Porta de proxy HTTP**. Por exemplo, defina demasiado**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Reinicie o agente de Olá.

  ```
  sudo service waagent restart
  ```

Olá, definições de proxy no \\etc\\waagent.conf também se aplicam as extensões VM toohello necessário. Se quiser toouse Olá repositórios do Azure, certifique-se de que repositórios de toothese Olá tráfego não for através da sua intranet local. Se tiver criado definido pelo utilizador rotas tooenable imposição do túnel, certifique-se de que o adicione uma rota que encaminha repositórios de toohello tráfego toohello diretamente à Internet e não através da ligação de VPN de site para site.

* **SLES**

  Terá também as rotas de tooadd para endereços IP Olá listadas em \\etc\\regionserverclnt.cfg. Olá figura seguinte mostra um exemplo:

  ![Túnel forçado][deployment-guide-figure-50]


* **RHEL**

  Terá também as rotas de tooadd para endereços IP de Olá dos anfitriões Olá listadas em \\etc\\yum.repos.d\\balanceadores de carga rhui. Por exemplo, consulte Olá precedente figura.

Para obter mais informações sobre as rotas definidas pelo utilizador, consulte [rotas definidas pelo utilizador e reencaminhamento IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configurar Olá Azure avançada extensão de monitorização para SAP
Quando já preparou Olá VM conforme descrito em [cenários de implementação de VMs para SAP no Azure][deployment-guide-3], Olá agente da VM do Azure está instalado na máquina virtual de Olá. Olá passo seguinte consiste em toodeploy Olá Azure avançada extensão de monitorização para SAP, que está disponível no Olá repositório de extensão do Azure em Olá centros de dados global do Azure. Para obter mais informações, consulte [Virtual Machines do Azure de planeamento e implementação de SAP no Linux][planning-guide-9.1].

Pode utilizar o PowerShell ou a CLI do Azure tooinstall e configurar Olá Azure avançada extensão de monitorização para SAP. extensão de Olá tooinstall num Windows ou VM com Linux através da utilização de um computador Windows, consulte [Azure PowerShell][deployment-guide-4.5.1]. extensão de Olá tooinstall numa VM com Linux através da utilização de um ambiente de trabalho do Linux, consulte [CLI do Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>O Azure PowerShell para Linux e VMs do Windows
tooinstall Olá Azure avançada extensão de monitorização para SAP através do PowerShell:

1. Certifique-se de que instalou a versão mais recente do Olá do cmdlet do Olá do Azure PowerShell. Para obter mais informações, consulte [cmdlets de implementação do Azure PowerShell][deployment-guide-4.1].  
2. Execute Olá seguinte cmdlet do PowerShell.
  Para obter uma lista dos ambientes disponíveis, execute `commandlet Get-AzureRmEnvironment`. Se quiser toouse Azure público, o seu ambiente é **AzureCloud**. Para o Azure na China, selecione **AzureChinaCloud**.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

Depois de introduzir os seus dados de conta e identificar Olá máquina virtual do Azure, o script de Olá implementa extensões Olá necessário e permite funcionalidades de Olá necessário. Isto pode demorar vários minutos.
Para obter mais informações sobre `Set-AzureRmVMAEMExtension`, consulte [conjunto AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![A execução com êxito do SAP específicos do Azure cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Olá `Set-AzureRmVMAEMExtension` configuração todos os anfitriões de tooconfigure do passos Olá monitorização para SAP.

resultado do script Olá inclui Olá seguintes informações:

* Confirmação de que a monitorização para Olá base VHD (com Olá SO) e todos os VHDs adicionais montado toohello que VM tenha sido configurada.
* mensagens Hello do dois confirme a configuração de Olá das métricas de armazenamento para uma conta de armazenamento específico.
* Uma linha de saída dá-estado de Olá da atualização real de Olá da configuração de monitorização de Olá.
* Outra linha do resultado confirma que a configuração Olá foi implementada ou atualizada.
* Olá a última linha do resultado é meramente informativa. Mostra as opções de teste configuração de monitorização de Olá.

toocheck que todos os passos do Azure avançada monitorização foram executados com êxito e que Olá infraestrutura do Azure fornece dados necessários Olá, continuar com a verificação de disponibilidade de Olá para Olá Azure avançada extensão de monitorização para SAP, conforme descrito em [Verificação de disponibilidade para avançada monitorização do Azure para SAP][deployment-guide-5.1]. Aguarde 15-30 minutos para dados relevantes do diagnóstico do Azure toocollect Olá.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>CLI do Azure para VMs com Linux
tooinstall Olá Azure avançada extensão de monitorização para SAP utilizando a CLI do Azure:

1. Instalar a CLI do Azure, conforme descrito em [instalação Olá CLI do Azure][azure-cli].
2. Inicie sessão com a sua conta do Azure:

  ```
  azure login
  ```

3. Modo do comutador tooAzure Resource Manager:

  ```
  azure config mode arm
  ```

4. Ative a monitorização avançada do Azure:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Certifique-se de que Olá extensão de monitorização avançada da Azure está ativa no Olá VM do Linux do Azure. Verifique se Olá ficheiro \\var\\lib\\AzureEnhancedMonitor\\PerfCounters existe. Se existir, numa linha de comandos, execute estas informações de toodisplay comando recolhidas pelo Olá Monitor avançada do Azure:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

saída de Olá tem o seguinte aspeto:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Verificações e a resolução de problemas para a monitorização ponto a ponto
Depois de ter implementado a VM do Azure e configurar a infraestrutura de monitorização do Azure relevantes Olá, verifique se todos os componentes de Olá de Olá extensão de monitorização avançada da Azure estão a funcionar conforme esperado.

Executar verificação de disponibilidade de Olá para Olá Azure avançada extensão de monitorização para SAP conforme descrito em [verificação de disponibilidade para Olá Azure avançada extensão de monitorização para SAP][deployment-guide-5.1]. Se todos os resultados da verificação de preparação estão positivo e relevantes todos os contadores de desempenho são apresentados OK, a monitorização do Azure configurada com êxito. Para poder continuar com a instalação de Olá do agente de anfitrião do SAP descrito nas notas de SAP Olá no [recursos SAP][deployment-guide-2.2]. Se a verificação de disponibilidade de Olá indica que os contadores estão em falta, execute a verificação de estado de funcionamento de Olá de Olá infraestrutura de monitorização do Azure, conforme descrito em [verificação de estado de funcionamento de configuração da infraestrutura de monitorização do Azure] [ deployment-guide-5.2]. Para obter mais opções de resolução de problemas, consulte [monitorização do Azure de resolução de problemas para SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Verificação de disponibilidade para Olá Azure avançada extensão de monitorização para SAP
Esta verificação certifica-se de que todas as métricas de desempenho que são apresentados no interior da sua aplicação de SAP são fornecidas pelo Olá subjacente monitorizar a infraestrutura do Azure.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Executar verificação de disponibilidade de Olá numa VM do Windows

1.  Inicie sessão no toohello máquina virtual do Azure (utilizar uma conta de administrador não é necessário).
2.  Abra uma janela de linha de comandos.
3.  Na linha de comandos Olá, alterar a pasta de instalação do Olá diretório toohello de Olá Azure avançada extensão de monitorização para SAP: c:\\pacotes\\plug-ins\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versão >\\drop

  Olá *versão* no Olá caminho toohello pode variar de extensão de monitorização. Se vir pastas para várias versões do Olá monitorização extensão na pasta de instalação de Olá, verifique a configuração de Olá de Olá serviço AzureEnhancedMonitoring Windows, e, em seguida, o comutador toohello pasta indicados como *tooexecutable de caminho* .

  ![Propriedades da execução do serviço Olá Azure avançada extensão de monitorização para SAP][deployment-guide-figure-1000]

4.  Na linha de comandos Olá, execute **azperflib.exe** sem quaisquer parâmetros.

  > [!NOTE]
  > Azperflib.exe é executado em ciclo e atualizações de contadores de Olá recolhido 60 em 60 segundos. tooend Olá ciclo, provocando uma janela de linha de comandos Olá fechar.
  >
  >

Se Olá que extensão de monitorização avançada da Azure não está instalado ou Olá AzureEnhancedMonitoring serviço não está em execução, a extensão de Olá não foi configurada corretamente. Para obter informações detalhadas sobre como toodeploy Olá extensão, consulte [resolução de problemas hello monitorização de infraestrutura do Azure para SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Verificar o resultado Olá azperflib.exe
Saída de Azperflib.exe mostra que todos os preenchido contadores de desempenho do Azure para SAP. Em Olá parte inferior da lista de Olá dos contadores recolhidos, um indicador de estado de funcionamento e o resumo Mostrar estado Olá de monitorização do Azure.

![Resultado da verificação de estado de funcionamento executando azperflib.exe, que indica que existem sem problemas][deployment-guide-figure-1100]
<a name="figure-11"></a>

Verificar o resultado de Olá devolvido para Olá **total contadores** resultado, o que é comunicado como vazio e para **o estado de funcionamento**, mostrado na Olá precedente figura.

Interpretar os valores de resultante Olá da seguinte forma:

| Valores de resultado Azperflib.exe | Monitorização de estado de funcionamento do Azure |
| --- | --- |
| **Chamadas à API - não disponível** | Os contadores que não estão disponíveis poderão ser a configuração da máquina virtual não aplicável toohello ou erros. Consulte **o estado de funcionamento**. |
| **Total de contadores - vazio** |Olá seguir dois contadores de armazenamento do Azure pode estar vazio: <ul><li>Armazenamento ler Op latência mseg de servidor</li><li>Armazenamento ler Op latência E2E MS</li></ul>Todos os outros contadores tem de ter valores. |
| **Estado de funcionamento** |Se apenas OK devolver o estado Mostrar **OK**. |
| **Diagnóstico** |Obter informações detalhadas sobre o estado de funcionamento. |

Se hello **o estado de funcionamento** valor não é **OK**, siga as instruções de Olá em [verificação de estado de funcionamento de configuração da infraestrutura de monitorização do Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Executar verificação de disponibilidade de Olá numa VM com Linux

1.  Liga toohello Máquina Virtual do Azure através de SSH.

2.  Verifique o resultado Olá Olá extensão de monitorização avançada da Azure.

  a.  Execute `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Era esperado o resultado**: lista de devolve dos contadores de desempenho. ficheiro de Olá não deve estar vazio.

 b. Execute `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Era esperado o resultado**: uma linha de devolve onde está o erro de Olá **nenhum**, por exemplo, **3; config; Erro; 0; 0; Nenhum; 0 1456416792; tst-servercs;**

  c. Execute `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Era esperado o resultado**: devolve como vazio ou não existe.

Se hello verificação anterior não foi bem sucedida, execute estes verificações adicionais:

1.  Certifique-se de que waagent Olá está instalado e ativado.

  a.  Execute `sudo ls -al /var/lib/waagent/`

      **Era esperado o resultado**: apresenta uma lista de conteúdo de Olá do diretório de waagent Olá.

  b.  Execute `ps -ax | grep waagent`

   **Era esperado o resultado**: apresenta uma entrada semelhante a:`python /usr/sbin/waagent -daemon`

2. Certifique-se de que Olá extensão de diagnóstico de Linux está instalado e ativado.

  a.  Execute `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`

   **Era esperado o resultado**: apresenta uma lista de conteúdo de Olá do diretório da extensão de diagnóstico do Linux Olá.

 b. Execute `ps -ax | grep diagnostic`

   **Era esperado o resultado**: apresenta uma entrada semelhante a:`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   Certifique-se de que Olá extensão de monitorização avançada da Azure está instalado e em execução.

  a.  Execute `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`

    **Era esperado o resultado**: apresenta uma lista de conteúdo de Olá do diretório de extensão de monitorização avançada da Azure Olá.

  b. Execute `ps -ax | grep AzureEnhanced`

     **Era esperado o resultado**: apresenta uma entrada semelhante a:`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Instalar o agente do anfitrião SAP, conforme descrito na nota SAP [1031096]e verificar o resultado Olá `saposcol`.

  a.  Execute `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Execute `dump ccm`

  c.  Verifique se Olá **Virtualization_Configuration\Enhanced monitorização acesso** métrica é **verdadeiro**.

Se já tiver um servidor de aplicações do SAP NetWeaver ABAP instalado, abra a transação ST06 e verificar se a monitorização avançada está ativada.

Se qualquer uma destas verificações falhar e para obter informações detalhadas sobre como tooredeploy Olá extensão, consulte [resolução de problemas hello monitorização de infraestrutura do Azure para SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Verificação de estado de funcionamento para Olá configuração da infraestrutura de monitorização do Azure
Se alguns dos dados de monitorização de Olá não for entregue corretamente conforme indicado pelo teste Olá descrita [verificação de disponibilidade para avançada monitorização do Azure para SAP][deployment-guide-5.1], hello execute `Test-AzureRmVMAEMExtension` cmdlet toocheck Indica se hello monitorização de infraestrutura e Olá extensão de monitorização para SAP do Azure está configurado corretamente.

1.  Certifique-se de que instalou a versão mais recente do Olá do cmdlet do PowerShell do Azure Olá, conforme descrito em [cmdlets de implementação do Azure PowerShell][deployment-guide-4.1].
2.  Execute Olá seguinte cmdlet do PowerShell. Para obter uma lista dos ambientes disponíveis, execute o cmdlet Olá `Get-AzureRmEnvironment`. Selecione do Azure, pública toouse Olá **AzureCloud** ambiente. Para o Azure na China, selecione **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Introduza os seus dados de conta e identificar Olá máquina virtual do Azure.

  ![Página de entrada do SAP específicos do Azure cmdlet VMConfigForSAP_GUI de teste][deployment-guide-figure-1200]

4. Olá script testes Olá configuração Olá máquina virtual que selecionar.

  ![Resultado do teste concluída com êxito de Olá monitorização de infraestrutura do Azure para SAP][deployment-guide-figure-1300]

Certifique-se de que todos os resultados da verificação de estado de funcionamento **OK**. Se não for apresentado algumas verificações **OK**, execute o cmdlet de atualização de Olá conforme descrito em [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5]. Aguarde 15 minutos e verificações de repetições Olá descritas na [verificação de disponibilidade para avançada monitorização do Azure para SAP] [ deployment-guide-5.1] e [verificação de estado de funcionamento de configuração da infraestrutura de monitorização de Azure] [deployment-guide-5.2]. Se as verificações de Olá ainda indicarem um problema com alguns ou todos os contadores, consulte o artigo [resolução de problemas hello monitorização de infraestrutura do Azure para SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Resolução de problemas Olá monitorização de infraestrutura do Azure para SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Contadores de desempenho do Azure não apresentada em todas as
Olá serviço AzureEnhancedMonitoring Windows recolhe métricas de desempenho no Azure. Se o serviço de Olá não foi instalado corretamente ou não está em execução na sua VM, a não haver métricas de desempenho podem ser recolhidas.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>diretório de instalação de Olá de Olá extensão de monitorização avançada da Azure está vazio

###### <a name="issue"></a>Problema
o diretório de instalação de Olá c:\\pacotes\\plug-ins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versão >\\largar está vazio.

###### <a name="solution"></a>Solução
extensão de Olá não está instalado. Determine se se trata de um problema de proxy (como descrito anteriormente). Poderá ser necessário da toorestart Olá máquina ou execute novamente Olá `Set-AzureRmVMAEMExtension` script de configuração.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Serviço para monitorização avançada do Azure não existe

###### <a name="issue"></a>Problema
Olá serviço AzureEnhancedMonitoring Windows não existe.

Saída de Azperflib.exe emite um erro:

![A execução do azperflib.exe indica que o serviço de Olá de Olá extensão de monitorização avançada da Azure para SAP não está em execução][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Solução
Se o serviço de Olá não existe, Olá Azure avançada extensão de monitorização para SAP não foi instalado corretamente. Reimplementar a extensão de Olá, utilizando os passos de Olá descritos para o seu cenário de implementação no [cenários de implementação de VMs para SAP no Azure][deployment-guide-3].

Depois de implementar extensão Olá, depois de uma hora, verifique novamente se os contadores de desempenho do Azure de Olá são fornecidos na Olá VM do Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Serviço para monitorização avançada do Azure existe, mas falha toostart

###### <a name="issue"></a>Problema
Olá serviço AzureEnhancedMonitoring Windows existe e está ativada, mas falha toostart. Para obter mais informações, verifique o registo de eventos de aplicações de Olá.

###### <a name="solution"></a>Solução
configuração de Olá está incorreta. Reiniciar Olá monitorização extensão para Olá VM, conforme descrito em [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Faltam alguns contadores de desempenho do Azure
Olá serviço AzureEnhancedMonitoring Windows recolhe métricas de desempenho no Azure. serviço de Olá obtém dados de várias origens. Alguns dados de configuração são recolhidos localmente, e algumas métricas de desempenho são lidos a partir do diagnóstico do Azure. Os contadores de armazenamento são utilizados a partir do seu registo no nível de subscrição de armazenamento Olá.

Se a resolução de problemas ao utilizar a nota SAP [1999351] não resolver o problema de Olá, volte a executar Olá `Set-AzureRmVMAEMExtension` script de configuração. Poderá ter toowait uma hora, porque os contadores de análise ou diagnósticos de armazenamento não podem ser criados imediatamente após estão ativadas. Se Olá problema persistir, abra uma mensagem de suporte de cliente SAP no Olá componente BC OP-NT AZR para Windows ou BC-OP-LNX-AZR para uma máquina virtual Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Contadores de desempenho do Azure não apresentada em todas as
Métricas de desempenho no Azure são recolhidas por um daemon. Se o daemon de Olá não está em execução, não haver métricas de desempenho podem ser recolhidas.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>diretório de instalação de Olá de Olá extensão avançada monitorização do Azure está vazio

###### <a name="issue"></a>Problema
diretório de Olá \\var\\lib\\waagent\\ não tem um subdiretório para Olá extensão avançada monitorização do Azure.

###### <a name="solution"></a>Solução
extensão de Olá não está instalado. Determine se se trata de um problema de proxy (como descrito anteriormente). Poderá ter de máquina de Olá toorestart e/ou volte a executar Olá `Set-AzureRmVMAEMExtension` script de configuração.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Faltam alguns contadores de desempenho do Azure
Métricas de desempenho no Azure são recolhidas por um daemon, que obtém dados de várias origens. Alguns dados de configuração são recolhidos localmente, e algumas métricas de desempenho são lidos a partir do diagnóstico do Azure. Os contadores de armazenamento provenientes Olá registos na sua subscrição de armazenamento.

Para obter uma lista completa e atualizada dos problemas conhecidos, consulte a nota SAP [1999351], que tem informações adicionais de resolução de problemas de avançada monitorização do Azure para SAP.

Se a resolução de problemas ao utilizar a nota SAP [1999351] não resolver o problema de Olá, volte a executar Olá `Set-AzureRmVMAEMExtension` script de configuração conforme descrito em [configurar Olá Azure avançada extensão de monitorização para SAP][deployment-guide-4.5]. Poderá ter toowait para uma hora, porque os contadores de análise ou diagnósticos de armazenamento não podem ser criados imediatamente após estão ativadas. Se Olá problema persistir, abra uma mensagem de suporte de cliente SAP no Olá componente BC OP-NT AZR para Windows ou BC-OP-LNX-AZR para uma máquina virtual Linux.
