---
title: Azure Virtual Machines deployment for SAP NetWeaver | Microsoft Docs
description: Learn how to deploy SAP software on Linux virtual machines in Azure.
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: ''
author: MSSedusch
manager: jeconnoc
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 43b4fb47b67abc33a031b7ef516e3eed33d11931
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826891"
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a><span data-ttu-id="1d2e4-103">Azure Virtual Machines deployment for SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="1d2e4-103">Azure Virtual Machines deployment for SAP NetWeaver</span></span>
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-cli-2]:https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from the Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics to SQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
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

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from the Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM to an on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable the Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure the Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for the Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure the proxy)
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
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmaemextension

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on the on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with the on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises to Azure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../networking/network-overview.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
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
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../extensions/agent-windows.md
[virtual-machines-linux-agent-user-guide]:../../extensions/agent-linux.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../extensions/agent-linux.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
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
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
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
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/template-samples.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/manage-virtual-network.md#create-a-virtual-network
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-network-deploy-multinic-classic-ps.md
[virtual-networks-nsg]:../../../virtual-network/security-overview.md
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

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="1d2e4-186">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-186">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="1d2e4-187">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-187">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="1d2e4-188">Extend an application's reliability and availability without additional on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-188">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="1d2e4-189">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-189">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="1d2e4-190">In this article, we cover the steps to deploy SAP applications on virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-190">In this article, we cover the steps to deploy SAP applications on virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span></span> <span data-ttu-id="1d2e4-191">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-191">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="1d2e4-192">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-192">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d2e4-193">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d2e4-193">Prerequisites</span></span>
<span data-ttu-id="1d2e4-194">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-194">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="1d2e4-195">Before you start, make sure that you meet the prerequisites for installing SAP software on virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-195">Before you start, make sure that you meet the prerequisites for installing SAP software on virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="1d2e4-196">Local computer</span><span class="sxs-lookup"><span data-stu-id="1d2e4-196">Local computer</span></span>
<span data-ttu-id="1d2e4-197">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-197">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span></span> <span data-ttu-id="1d2e4-198">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-198">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="1d2e4-199">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-199">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="1d2e4-200">Internet connection</span><span class="sxs-lookup"><span data-stu-id="1d2e4-200">Internet connection</span></span>
<span data-ttu-id="1d2e4-201">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-201">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span></span> <span data-ttu-id="1d2e4-202">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-202">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span></span> <span data-ttu-id="1d2e4-203">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-203">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="1d2e4-204">Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="1d2e4-204">Microsoft Azure subscription</span></span>
<span data-ttu-id="1d2e4-205">You need an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-205">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="1d2e4-206">Topology and networking</span><span class="sxs-lookup"><span data-stu-id="1d2e4-206">Topology and networking</span></span>
<span data-ttu-id="1d2e4-207">You need to define the topology and architecture of the SAP deployment in Azure:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-207">You need to define the topology and architecture of the SAP deployment in Azure:</span></span>

* <span data-ttu-id="1d2e4-208">Azure storage accounts to be used</span><span class="sxs-lookup"><span data-stu-id="1d2e4-208">Azure storage accounts to be used</span></span>
* <span data-ttu-id="1d2e4-209">Virtual network where you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="1d2e4-209">Virtual network where you want to deploy the SAP system</span></span>
* <span data-ttu-id="1d2e4-210">Resource group to which you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="1d2e4-210">Resource group to which you want to deploy the SAP system</span></span>
* <span data-ttu-id="1d2e4-211">Azure region where you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="1d2e4-211">Azure region where you want to deploy the SAP system</span></span>
* <span data-ttu-id="1d2e4-212">SAP configuration (two-tier or three-tier)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-212">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="1d2e4-213">VM sizes and the number of additional data disks to be mounted to the VMs</span><span class="sxs-lookup"><span data-stu-id="1d2e4-213">VM sizes and the number of additional data disks to be mounted to the VMs</span></span>
* <span data-ttu-id="1d2e4-214">SAP Correction and Transport System (CTS) configuration</span><span class="sxs-lookup"><span data-stu-id="1d2e4-214">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="1d2e4-215">Create and configure Azure storage accounts (if required) or Azure virtual networks before you begin the SAP software deployment process.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-215">Create and configure Azure storage accounts (if required) or Azure virtual networks before you begin the SAP software deployment process.</span></span> <span data-ttu-id="1d2e4-216">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-216">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="1d2e4-217">SAP sizing</span><span class="sxs-lookup"><span data-stu-id="1d2e4-217">SAP sizing</span></span>
<span data-ttu-id="1d2e4-218">Know the following information, for SAP sizing:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-218">Know the following information, for SAP sizing:</span></span>

* <span data-ttu-id="1d2e4-219">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span><span class="sxs-lookup"><span data-stu-id="1d2e4-219">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="1d2e4-220">Required CPU resource and memory consumption of the SAP system</span><span class="sxs-lookup"><span data-stu-id="1d2e4-220">Required CPU resource and memory consumption of the SAP system</span></span>
* <span data-ttu-id="1d2e4-221">Required input/output (I/O) operations per second</span><span class="sxs-lookup"><span data-stu-id="1d2e4-221">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="1d2e4-222">Required network bandwidth of eventual communication between VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="1d2e4-222">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="1d2e4-223">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span><span class="sxs-lookup"><span data-stu-id="1d2e4-223">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="1d2e4-224">Resource groups</span><span class="sxs-lookup"><span data-stu-id="1d2e4-224">Resource groups</span></span>
<span data-ttu-id="1d2e4-225">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-225">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="1d2e4-226">For more information, see [Azure Resource Manager overview][resource-group-overview].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-226">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="1d2e4-227">Resources</span><span class="sxs-lookup"><span data-stu-id="1d2e4-227">Resources</span></span>

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a><span data-ttu-id="1d2e4-228">SAP resources</span><span class="sxs-lookup"><span data-stu-id="1d2e4-228">SAP resources</span></span>
<span data-ttu-id="1d2e4-229">When you are setting up your SAP software deployment, you need the following SAP resources:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-229">When you are setting up your SAP software deployment, you need the following SAP resources:</span></span>

* <span data-ttu-id="1d2e4-230">SAP Note [1928533], which has:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-230">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="1d2e4-231">List of Azure VM sizes that are supported for the deployment of SAP software</span><span class="sxs-lookup"><span data-stu-id="1d2e4-231">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="1d2e4-232">Important capacity information for Azure VM sizes</span><span class="sxs-lookup"><span data-stu-id="1d2e4-232">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="1d2e4-233">Supported SAP software, and operating system (OS) and database combinations</span><span class="sxs-lookup"><span data-stu-id="1d2e4-233">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="1d2e4-234">Required SAP kernel version for Windows and Linux on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1d2e4-234">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="1d2e4-235">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-235">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="1d2e4-236">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-236">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="1d2e4-237">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-237">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="1d2e4-238">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-238">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="1d2e4-239">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-239">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="1d2e4-240">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-240">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="1d2e4-241">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-241">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="1d2e4-242">SAP Note [2069760] has general information about Oracle Linux 7.x.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-242">SAP Note [2069760] has general information about Oracle Linux 7.x.</span></span>
* <span data-ttu-id="1d2e4-243">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-243">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="1d2e4-244">SAP Note [1597355] has general information about swap-space for Linux.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-244">SAP Note [1597355] has general information about swap-space for Linux.</span></span>
* <span data-ttu-id="1d2e4-245">[SAP on Azure SCN page](https://wiki.scn.sap.com/wiki/x/Pia7Gg) has news and a collection of useful resources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-245">[SAP on Azure SCN page](https://wiki.scn.sap.com/wiki/x/Pia7Gg) has news and a collection of useful resources.</span></span>
* <span data-ttu-id="1d2e4-246">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-246">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="1d2e4-247">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-247">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="1d2e4-248">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-248">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a><span data-ttu-id="1d2e4-249">Windows resources</span><span class="sxs-lookup"><span data-stu-id="1d2e4-249">Windows resources</span></span>
<span data-ttu-id="1d2e4-250">These Microsoft articles cover SAP deployments in Azure:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-250">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="1d2e4-251">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-251">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="1d2e4-252">[Azure Virtual Machines deployment for SAP NetWeaver (this article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-252">[Azure Virtual Machines deployment for SAP NetWeaver (this article)][deployment-guide]</span></span>
* <span data-ttu-id="1d2e4-253">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-253">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a><span data-ttu-id="1d2e4-254">Deployment scenarios for SAP software on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="1d2e4-254">Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="1d2e4-255">You have multiple options for deploying VMs and associated disks in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-255">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="1d2e4-256">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-256">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span></span>

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a><span data-ttu-id="1d2e4-257">Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-257">Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span></span>
<span data-ttu-id="1d2e4-258">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-258">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span></span> <span data-ttu-id="1d2e4-259">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-259">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="1d2e4-260">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-260">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="1d2e4-261">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-261">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>

<span data-ttu-id="1d2e4-262">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-262">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM image from the Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="1d2e4-264">Create a virtual machine by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d2e4-264">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="1d2e4-265">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-265">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span></span>

1.  <span data-ttu-id="1d2e4-266">Go to <https://portal.azure.com/#create/hub>.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-266">Go to <https://portal.azure.com/#create/hub>.</span></span>  <span data-ttu-id="1d2e4-267">Or, in the Azure portal menu, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-267">Or, in the Azure portal menu, select **+ New**.</span></span>
1.  <span data-ttu-id="1d2e4-268">Select **Compute**, and then select the type of operating system you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-268">Select **Compute**, and then select the type of operating system you want to deploy.</span></span> <span data-ttu-id="1d2e4-269">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-269">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span> <span data-ttu-id="1d2e4-270">The default list view does not show all supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-270">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="1d2e4-271">Select **see all** for a full list.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-271">Select **see all** for a full list.</span></span> <span data-ttu-id="1d2e4-272">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-272">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
1.  <span data-ttu-id="1d2e4-273">On the next page, review terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-273">On the next page, review terms and conditions.</span></span>
1.  <span data-ttu-id="1d2e4-274">In the **Select a deployment model** box, select **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-274">In the **Select a deployment model** box, select **Resource Manager**.</span></span>
1.  <span data-ttu-id="1d2e4-275">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-275">Select **Create**.</span></span>

<span data-ttu-id="1d2e4-276">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-276">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="1d2e4-277">Some of these parameters are:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-277">Some of these parameters are:</span></span>

1. <span data-ttu-id="1d2e4-278">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-278">**Basics**:</span></span>
 * <span data-ttu-id="1d2e4-279">**Name**: The name of the resource (the virtual machine name).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-279">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="1d2e4-280">**VM disk type**: Select the disk type of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-280">**VM disk type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="1d2e4-281">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-281">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
 * <span data-ttu-id="1d2e4-282">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-282">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="1d2e4-283">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-283">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="1d2e4-284">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-284">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="1d2e4-285">**Resource group**: The name of the resource group for the VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-285">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="1d2e4-286">You can enter either the name of a new resource group or the name of a resource group that already exists.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-286">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="1d2e4-287">**Location**: Where to deploy the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-287">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="1d2e4-288">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-288">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="1d2e4-289">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-289">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
1. <span data-ttu-id="1d2e4-290">**Size**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-290">**Size**:</span></span>

     <span data-ttu-id="1d2e4-291">For a list of supported VM types, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-291">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="1d2e4-292">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-292">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="1d2e4-293">Not all VM types support Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-293">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="1d2e4-294">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-294">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

1. <span data-ttu-id="1d2e4-295">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-295">**Settings**:</span></span>
  * <span data-ttu-id="1d2e4-296">**Storage**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-296">**Storage**</span></span>
    * <span data-ttu-id="1d2e4-297">**Disk Type**: Select the disk type of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-297">**Disk Type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="1d2e4-298">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-298">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
    * <span data-ttu-id="1d2e4-299">**Use managed disks**: If you want to use Managed Disks, select Yes.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-299">**Use managed disks**: If you want to use Managed Disks, select Yes.</span></span> <span data-ttu-id="1d2e4-300">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-300">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span></span>
    * <span data-ttu-id="1d2e4-301">**Storage account**: Select an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-301">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="1d2e4-302">Not all storage types work for running SAP applications.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-302">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="1d2e4-303">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-303">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span>
  * <span data-ttu-id="1d2e4-304">**Network**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-304">**Network**</span></span>
    * <span data-ttu-id="1d2e4-305">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-305">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
    * <span data-ttu-id="1d2e4-306">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-306">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="1d2e4-307">You can use a public IP address to access your virtual machine over the Internet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-307">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="1d2e4-308">Make sure that you also create a network security group to help secure access to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-308">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
    * <span data-ttu-id="1d2e4-309">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-309">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="1d2e4-310">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-310">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span></span> <span data-ttu-id="1d2e4-311">You do not need to add extensions in this step.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-311">You do not need to add extensions in this step.</span></span> <span data-ttu-id="1d2e4-312">The extensions required for SAP support are installed later.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-312">The extensions required for SAP support are installed later.</span></span> <span data-ttu-id="1d2e4-313">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-313">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="1d2e4-314">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-314">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="1d2e4-315">For more information, see [Azure availability sets][planning-guide-3.2.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-315">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="1d2e4-316">**Monitoring**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-316">**Monitoring**</span></span>
    * <span data-ttu-id="1d2e4-317">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-317">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="1d2e4-318">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-318">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

1. <span data-ttu-id="1d2e4-319">**Summary**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-319">**Summary**:</span></span>

  <span data-ttu-id="1d2e4-320">Review your selections, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-320">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="1d2e4-321">Your virtual machine is deployed in the resource group you selected.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-321">Your virtual machine is deployed in the resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="1d2e4-322">Create a virtual machine by using a template</span><span class="sxs-lookup"><span data-stu-id="1d2e4-322">Create a virtual machine by using a template</span></span>
<span data-ttu-id="1d2e4-323">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-323">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1d2e4-324">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-324">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="1d2e4-325">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-325">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="1d2e4-326">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-326">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1d2e4-327">[**Two-tier configuration (only one virtual machine) template - Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-327">[**Two-tier configuration (only one virtual machine) template - Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="1d2e4-328">To create a two-tier system by using only one virtual machine and Managed Disks, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-328">To create a two-tier system by using only one virtual machine and Managed Disks, use this template.</span></span>
* <span data-ttu-id="1d2e4-329">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-329">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="1d2e4-330">To create a three-tier system by using multiple virtual machines, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-330">To create a three-tier system by using multiple virtual machines, use this template.</span></span>
* <span data-ttu-id="1d2e4-331">[**Three-tier configuration (multiple virtual machines) template - Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-331">[**Three-tier configuration (multiple virtual machines) template - Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]</span></span>

  <span data-ttu-id="1d2e4-332">To create a three-tier system by using multiple virtual machines and Managed Disks, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-332">To create a three-tier system by using multiple virtual machines and Managed Disks, use this template.</span></span>

<span data-ttu-id="1d2e4-333">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-333">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="1d2e4-334">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-334">**Basics**:</span></span>
  * <span data-ttu-id="1d2e4-335">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-335">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="1d2e4-336">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-336">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="1d2e4-337">You can create a new resource group, or you can select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-337">You can create a new resource group, or you can select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="1d2e4-338">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-338">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="1d2e4-339">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-339">If you selected an existing resource group, the location of that resource group is used.</span></span>

1. <span data-ttu-id="1d2e4-340">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-340">**Settings**:</span></span>
  * <span data-ttu-id="1d2e4-341">**SAP System ID**: The SAP System ID (SID).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-341">**SAP System ID**: The SAP System ID (SID).</span></span>
  * <span data-ttu-id="1d2e4-342">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-342">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2), or Oracle Linux 7.2.</span></span>

    <span data-ttu-id="1d2e4-343">The list view does not show all supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-343">The list view does not show all supported operating systems.</span></span> <span data-ttu-id="1d2e4-344">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-344">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="1d2e4-345">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-345">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="1d2e4-346">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-346">The number of SAPS the new system provides.</span></span> <span data-ttu-id="1d2e4-347">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-347">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1d2e4-348">**System availability** (three-tier template only): The system availability.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-348">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="1d2e4-349">Select **HA** for a configuration that is suitable for a high-availability installation.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-349">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="1d2e4-350">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-350">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="1d2e4-351">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-351">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="1d2e4-352">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-352">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1d2e4-353">For more information about storage types, see these resources:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-353">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="1d2e4-354">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-354">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1d2e4-355">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-355">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1d2e4-356">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-356">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1d2e4-357">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-357">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1d2e4-358">**Admin username** and **Admin password**: A username and password.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-358">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="1d2e4-359">A new user is created, for signing in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-359">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="1d2e4-360">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-360">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="1d2e4-361">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-361">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1d2e4-362">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-362">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span></span> <span data-ttu-id="1d2e4-363">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-363">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="1d2e4-364">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="1d2e4-364">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

1. <span data-ttu-id="1d2e4-365">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-365">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1d2e4-366">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-366">Review and accept the legal terms.</span></span>

1.  <span data-ttu-id="1d2e4-367">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-367">Select **Purchase**.</span></span>

<span data-ttu-id="1d2e4-368">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-368">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1d2e4-369">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="1d2e4-369">Configure proxy settings</span></span>
<span data-ttu-id="1d2e4-370">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-370">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="1d2e4-371">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-371">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="1d2e4-372">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-372">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1d2e4-373">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-373">Join a domain (Windows only)</span></span>
<span data-ttu-id="1d2e4-374">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-374">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="1d2e4-375">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-375">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a><span data-ttu-id="1d2e4-376">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="1d2e4-376">Configure monitoring</span></span>
<span data-ttu-id="1d2e4-377">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-377">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1d2e4-378">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-378">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1d2e4-379">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="1d2e4-379">Monitoring check</span></span>
<span data-ttu-id="1d2e4-380">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-380">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="1d2e4-381">Post-deployment steps</span><span class="sxs-lookup"><span data-stu-id="1d2e4-381">Post-deployment steps</span></span>
<span data-ttu-id="1d2e4-382">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-382">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span></span> <span data-ttu-id="1d2e4-383">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-383">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="1d2e4-384">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-384">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="1d2e4-385">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-385">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="1d2e4-386">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs or Managed Disks, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-386">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs or Managed Disks, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span></span>

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a><span data-ttu-id="1d2e4-387">Scenario 2: Deploying a VM with a custom image for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-387">Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="1d2e4-388">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-388">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="1d2e4-389">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-389">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="1d2e4-390">You use different steps to create a private image for Linux than to create one for Windows.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-390">You use different steps to create a private image for Linux than to create one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="1d2e4-392">Windows</span><span class="sxs-lookup"><span data-stu-id="1d2e4-392">Windows</span></span>
>
> <span data-ttu-id="1d2e4-393">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-393">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="1d2e4-394">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-394">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="1d2e4-396">Linux</span><span class="sxs-lookup"><span data-stu-id="1d2e4-396">Linux</span></span>
>
> <span data-ttu-id="1d2e4-397">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-397">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="1d2e4-398">You can use `waagent -deprovision`  to do this.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-398">You can use `waagent -deprovision`  to do this.</span></span> <span data-ttu-id="1d2e4-399">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-399">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="1d2e4-400">You can prepare and create a custom image, and then use it to create multiple new VMs.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-400">You can prepare and create a custom image, and then use it to create multiple new VMs.</span></span> <span data-ttu-id="1d2e4-401">This is described in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-401">This is described in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span> <span data-ttu-id="1d2e4-402">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a disk that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-402">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a disk that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="1d2e4-403">For more information, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-403">For more information, see [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide].</span></span> <span data-ttu-id="1d2e4-404">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-404">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="1d2e4-405">Otherwise, you can install the SAP software after you deploy the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-405">Otherwise, you can install the SAP software after you deploy the Azure VM.</span></span>

<span data-ttu-id="1d2e4-406">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-406">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM image in private Marketplace][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="1d2e4-408">Create a virtual machine by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d2e4-408">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="1d2e4-409">The easiest way to create a new virtual machine from a Managed Disk image is by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-409">The easiest way to create a new virtual machine from a Managed Disk image is by using the Azure portal.</span></span> <span data-ttu-id="1d2e4-410">For more information on how to create a Manage Disk Image, read [Capture a managed image of a generalized VM in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-410">For more information on how to create a Manage Disk Image, read [Capture a managed image of a generalized VM in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)</span></span>

1.  <span data-ttu-id="1d2e4-411">Go to <https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-411">Go to <https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>.</span></span> <span data-ttu-id="1d2e4-412">Or, in the Azure portal menu, select **Images**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-412">Or, in the Azure portal menu, select **Images**.</span></span>
1.  <span data-ttu-id="1d2e4-413">Select the Managed Disk image you want to deploy and click on **Create VM**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-413">Select the Managed Disk image you want to deploy and click on **Create VM**</span></span>

<span data-ttu-id="1d2e4-414">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-414">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="1d2e4-415">Some of these parameters are:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-415">Some of these parameters are:</span></span>

1. <span data-ttu-id="1d2e4-416">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-416">**Basics**:</span></span>
 * <span data-ttu-id="1d2e4-417">**Name**: The name of the resource (the virtual machine name).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-417">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="1d2e4-418">**VM disk type**: Select the disk type of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-418">**VM disk type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="1d2e4-419">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-419">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
 * <span data-ttu-id="1d2e4-420">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-420">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="1d2e4-421">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-421">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="1d2e4-422">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-422">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="1d2e4-423">**Resource group**: The name of the resource group for the VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-423">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="1d2e4-424">You can enter either the name of a new resource group or the name of a resource group that already exists.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-424">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="1d2e4-425">**Location**: Where to deploy the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-425">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="1d2e4-426">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-426">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="1d2e4-427">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-427">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>
1. <span data-ttu-id="1d2e4-428">**Size**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-428">**Size**:</span></span>

     <span data-ttu-id="1d2e4-429">For a list of supported VM types, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-429">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="1d2e4-430">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-430">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="1d2e4-431">Not all VM types support Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-431">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="1d2e4-432">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-432">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide].</span></span>

1. <span data-ttu-id="1d2e4-433">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-433">**Settings**:</span></span>
  * <span data-ttu-id="1d2e4-434">**Storage**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-434">**Storage**</span></span>
    * <span data-ttu-id="1d2e4-435">**Disk Type**: Select the disk type of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-435">**Disk Type**: Select the disk type of the OS disk.</span></span> <span data-ttu-id="1d2e4-436">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-436">If you want to use Premium Storage for your data disks, we recommend using Premium Storage for the OS disk as well.</span></span>
    * <span data-ttu-id="1d2e4-437">**Use managed disks**: If you want to use Managed Disks, select Yes.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-437">**Use managed disks**: If you want to use Managed Disks, select Yes.</span></span> <span data-ttu-id="1d2e4-438">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-438">For more information about Managed Disks, see chapter [Managed Disks][planning-guide-managed-disks] in the planning guide.</span></span>
  * <span data-ttu-id="1d2e4-439">**Network**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-439">**Network**</span></span>
    * <span data-ttu-id="1d2e4-440">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-440">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
    * <span data-ttu-id="1d2e4-441">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-441">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="1d2e4-442">You can use a public IP address to access your virtual machine over the Internet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-442">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="1d2e4-443">Make sure that you also create a network security group to help secure access to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-443">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
    * <span data-ttu-id="1d2e4-444">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-444">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
  * <span data-ttu-id="1d2e4-445">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-445">**Extensions**: You can install virtual machine extensions by adding them to the deployment.</span></span> <span data-ttu-id="1d2e4-446">You do not need to add extension in this step.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-446">You do not need to add extension in this step.</span></span> <span data-ttu-id="1d2e4-447">The extensions required for SAP support are installed later.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-447">The extensions required for SAP support are installed later.</span></span> <span data-ttu-id="1d2e4-448">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-448">See chapter [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5] in this guide.</span></span>
  * <span data-ttu-id="1d2e4-449">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-449">**High Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="1d2e4-450">For more information, see [Azure availability sets][planning-guide-3.2.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-450">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
  * <span data-ttu-id="1d2e4-451">**Monitoring**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-451">**Monitoring**</span></span>
    * <span data-ttu-id="1d2e4-452">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-452">**Boot diagnostics**: You can select **Disable** for boot diagnostics.</span></span>
    * <span data-ttu-id="1d2e4-453">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-453">**Guest OS diagnostics**: You can select **Disable** for monitoring diagnostics.</span></span>

1. <span data-ttu-id="1d2e4-454">**Summary**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-454">**Summary**:</span></span>

  <span data-ttu-id="1d2e4-455">Review your selections, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-455">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="1d2e4-456">Your virtual machine is deployed in the resource group you selected.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-456">Your virtual machine is deployed in the resource group you selected.</span></span>
#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="1d2e4-457">Create a virtual machine by using a template</span><span class="sxs-lookup"><span data-stu-id="1d2e4-457">Create a virtual machine by using a template</span></span>
<span data-ttu-id="1d2e4-458">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-458">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span></span> <span data-ttu-id="1d2e4-459">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-459">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1d2e4-460">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-460">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="1d2e4-461">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-461">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="1d2e4-462">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-462">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1d2e4-463">[**Two-tier configuration (only one virtual machine) template - Managed Disk Image** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-463">[**Two-tier configuration (only one virtual machine) template - Managed Disk Image** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]</span></span>

  <span data-ttu-id="1d2e4-464">To create a two-tier system by using only one virtual machine and a Managed Disk image, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-464">To create a two-tier system by using only one virtual machine and a Managed Disk image, use this template.</span></span>
* <span data-ttu-id="1d2e4-465">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-465">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="1d2e4-466">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-466">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>
* <span data-ttu-id="1d2e4-467">[**Three-tier configuration (multiple virtual machines) template - Managed Disk Image** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-467">[**Three-tier configuration (multiple virtual machines) template - Managed Disk Image** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]</span></span>

  <span data-ttu-id="1d2e4-468">To create a three-tier system by using multiple virtual machines or your own OS image and a Managed Disk image, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-468">To create a three-tier system by using multiple virtual machines or your own OS image and a Managed Disk image, use this template.</span></span>

<span data-ttu-id="1d2e4-469">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-469">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="1d2e4-470">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-470">**Basics**:</span></span>
  * <span data-ttu-id="1d2e4-471">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-471">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="1d2e4-472">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-472">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="1d2e4-473">You can create a new resource group or select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-473">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="1d2e4-474">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-474">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="1d2e4-475">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-475">If you selected an existing resource group, the location of that resource group is used.</span></span>
1. <span data-ttu-id="1d2e4-476">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-476">**Settings**:</span></span>
  * <span data-ttu-id="1d2e4-477">**SAP System ID**: The SAP System ID.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-477">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="1d2e4-478">**OS type**: The operating system type you want to deploy (Windows or Linux).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-478">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="1d2e4-479">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-479">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="1d2e4-480">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-480">The number of SAPS the new system provides.</span></span> <span data-ttu-id="1d2e4-481">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-481">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1d2e4-482">**System availability** (three-tier template only): The system availability.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-482">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="1d2e4-483">Select **HA** for a configuration that is suitable for a high-availability installation.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-483">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="1d2e4-484">Two database servers and two servers for ASCS are created.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-484">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="1d2e4-485">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-485">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="1d2e4-486">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-486">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1d2e4-487">For more information about storage types, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-487">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="1d2e4-488">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-488">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1d2e4-489">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-489">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1d2e4-490">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-490">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1d2e4-491">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-491">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1d2e4-492">**User image VHD URI** (unmanaged disk image template only): The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-492">**User image VHD URI** (unmanaged disk image template only): The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="1d2e4-493">**User image storage account** (unmanaged disk image template only): The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-493">**User image storage account** (unmanaged disk image template only): The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="1d2e4-494">**userImageId** (managed disk image template only): Id of the Managed Disk image you want to use</span><span class="sxs-lookup"><span data-stu-id="1d2e4-494">**userImageId** (managed disk image template only): Id of the Managed Disk image you want to use</span></span>
  * <span data-ttu-id="1d2e4-495">**Admin username** and **Admin password**: The username and password.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-495">**Admin username** and **Admin password**: The username and password.</span></span>

    <span data-ttu-id="1d2e4-496">A new user is created, for signing in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-496">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="1d2e4-497">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-497">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="1d2e4-498">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-498">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1d2e4-499">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-499">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="1d2e4-500">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-500">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="1d2e4-501">The ID usually looks like this:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-501">The ID usually looks like this:</span></span>

    <span data-ttu-id="1d2e4-502">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="1d2e4-502">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

1. <span data-ttu-id="1d2e4-503">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-503">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1d2e4-504">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-504">Review and accept the legal terms.</span></span>

1.  <span data-ttu-id="1d2e4-505">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-505">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent-linux-only"></a><span data-ttu-id="1d2e4-506">Install the VM Agent (Linux only)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-506">Install the VM Agent (Linux only)</span></span>
<span data-ttu-id="1d2e4-507">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-507">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span></span> <span data-ttu-id="1d2e4-508">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-508">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="1d2e4-509">If you don't use the templates, you also can install the VM Agent later.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-509">If you don't use the templates, you also can install the VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1d2e4-510">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-510">Join a domain (Windows only)</span></span>
<span data-ttu-id="1d2e4-511">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-511">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="1d2e4-512">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-512">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1d2e4-513">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="1d2e4-513">Configure proxy settings</span></span>
<span data-ttu-id="1d2e4-514">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-514">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="1d2e4-515">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-515">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="1d2e4-516">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-516">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="1d2e4-517">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="1d2e4-517">Configure monitoring</span></span>
<span data-ttu-id="1d2e4-518">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-518">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1d2e4-519">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-519">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1d2e4-520">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="1d2e4-520">Monitoring check</span></span>
<span data-ttu-id="1d2e4-521">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-521">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>


### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a><span data-ttu-id="1d2e4-522">Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-522">Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="1d2e4-523">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-523">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span></span> <span data-ttu-id="1d2e4-524">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-524">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span></span> <span data-ttu-id="1d2e4-525">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-525">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span></span> <span data-ttu-id="1d2e4-526">You do not need to generalize the OS.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-526">You do not need to generalize the OS.</span></span> <span data-ttu-id="1d2e4-527">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-527">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="1d2e4-528">In this scenario, the VM Agent is **not** automatically installed during deployment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-528">In this scenario, the VM Agent is **not** automatically installed during deployment.</span></span> <span data-ttu-id="1d2e4-529">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP are required to run SAP NetWeaver on Azure, you need to download, install, and enable both components manually after you create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-529">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP are required to run SAP NetWeaver on Azure, you need to download, install, and enable both components manually after you create the virtual machine.</span></span>

<span data-ttu-id="1d2e4-530">For more information about the Azure VM Agent, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-530">For more information about the Azure VM Agent, see the following resources.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="1d2e4-532">Windows</span><span class="sxs-lookup"><span data-stu-id="1d2e4-532">Windows</span></span>
>
> <span data-ttu-id="1d2e4-533">[Azure Virtual Machine Agent overview][virtual-machines-windows-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-533">[Azure Virtual Machine Agent overview][virtual-machines-windows-agent-user-guide]</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="1d2e4-535">Linux</span><span class="sxs-lookup"><span data-stu-id="1d2e4-535">Linux</span></span>
>
> <span data-ttu-id="1d2e4-536">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-536">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="1d2e4-537">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-537">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM disk][deployment-guide-figure-400]

<span data-ttu-id="1d2e4-539">If the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), do the tasks described in the next few sections.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-539">If the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), do the tasks described in the next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="1d2e4-540">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d2e4-540">Create a virtual machine</span></span>
<span data-ttu-id="1d2e4-541">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-541">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="1d2e4-542">You also can manually create a virtual machine, by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-542">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="1d2e4-543">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-543">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="1d2e4-544">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-544">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="1d2e4-545">[**Two-tier configuration (only one virtual machine) template - Managed Disk** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-545">[**Two-tier configuration (only one virtual machine) template - Managed Disk** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]</span></span>

  <span data-ttu-id="1d2e4-546">To create a two-tier system by using only one virtual machine and a Managed Disk, use this template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-546">To create a two-tier system by using only one virtual machine and a Managed Disk, use this template.</span></span>

<span data-ttu-id="1d2e4-547">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-547">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="1d2e4-548">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-548">**Basics**:</span></span>
  * <span data-ttu-id="1d2e4-549">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-549">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="1d2e4-550">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-550">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="1d2e4-551">You can create a new resource group or select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-551">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="1d2e4-552">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-552">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="1d2e4-553">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-553">If you selected an existing resource group, the location of that resource group is used.</span></span>
1. <span data-ttu-id="1d2e4-554">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-554">**Settings**:</span></span>
  * <span data-ttu-id="1d2e4-555">**SAP System ID**: The SAP System ID.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-555">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="1d2e4-556">**OS type**: The operating system type you want to deploy (Windows or Linux).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-556">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="1d2e4-557">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-557">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="1d2e4-558">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-558">The number of SAPS the new system provides.</span></span> <span data-ttu-id="1d2e4-559">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-559">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="1d2e4-560">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-560">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="1d2e4-561">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-561">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="1d2e4-562">For more information about storage types, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-562">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="1d2e4-563">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-563">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="1d2e4-564">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-564">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
      * <span data-ttu-id="1d2e4-565">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-565">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="1d2e4-566">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="1d2e4-566">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="1d2e4-567">**OS disk VHD URI** (unmanaged disk template only): The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-567">**OS disk VHD URI** (unmanaged disk template only): The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="1d2e4-568">**OS disk Managed Disk Id** (managed disk template only): The Id of the Managed Disk OS disk, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN</span><span class="sxs-lookup"><span data-stu-id="1d2e4-568">**OS disk Managed Disk Id** (managed disk template only): The Id of the Managed Disk OS disk, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN</span></span>
  * <span data-ttu-id="1d2e4-569">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-569">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="1d2e4-570">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-570">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="1d2e4-571">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-571">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="1d2e4-572">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-572">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="1d2e4-573">The ID usually looks like this:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-573">The ID usually looks like this:</span></span>

    <span data-ttu-id="1d2e4-574">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="1d2e4-574">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

1. <span data-ttu-id="1d2e4-575">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-575">**Terms and conditions**:</span></span>  
    <span data-ttu-id="1d2e4-576">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-576">Review and accept the legal terms.</span></span>

1.  <span data-ttu-id="1d2e4-577">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-577">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent"></a><span data-ttu-id="1d2e4-578">Install the VM Agent</span><span class="sxs-lookup"><span data-stu-id="1d2e4-578">Install the VM Agent</span></span>
<span data-ttu-id="1d2e4-579">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-579">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span></span> <span data-ttu-id="1d2e4-580">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-580">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="1d2e4-581">If you don't use the templates described in the preceding section, you can also install the VM Agent afterwards.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-581">If you don't use the templates described in the preceding section, you can also install the VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="1d2e4-582">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-582">Join a domain (Windows only)</span></span>
<span data-ttu-id="1d2e4-583">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-583">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="1d2e4-584">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-584">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="1d2e4-585">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="1d2e4-585">Configure proxy settings</span></span>
<span data-ttu-id="1d2e4-586">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-586">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="1d2e4-587">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-587">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="1d2e4-588">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-588">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="1d2e4-589">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="1d2e4-589">Configure monitoring</span></span>
<span data-ttu-id="1d2e4-590">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-590">To be sure SAP supports your environment, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1d2e4-591">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-591">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="1d2e4-592">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="1d2e4-592">Monitoring check</span></span>
<span data-ttu-id="1d2e4-593">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-593">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-the-monitoring-configuration-for-sap"></a><span data-ttu-id="1d2e4-594">Update the monitoring configuration for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-594">Update the monitoring configuration for SAP</span></span>
<span data-ttu-id="1d2e4-595">Update the SAP monitoring configuration in any of the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-595">Update the SAP monitoring configuration in any of the following scenarios:</span></span>
* <span data-ttu-id="1d2e4-596">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-596">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="1d2e4-597">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-597">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span></span>
* <span data-ttu-id="1d2e4-598">You mount additional data disks to your Azure VM or you remove a data disk.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-598">You mount additional data disks to your Azure VM or you remove a data disk.</span></span> <span data-ttu-id="1d2e4-599">In this scenario, update the collection of storage-related data.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-599">In this scenario, update the collection of storage-related data.</span></span> <span data-ttu-id="1d2e4-600">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-600">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span></span>
* <span data-ttu-id="1d2e4-601">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-601">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span></span>
* <span data-ttu-id="1d2e4-602">You add new network interfaces to your Azure VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-602">You add new network interfaces to your Azure VM.</span></span>

<span data-ttu-id="1d2e4-603">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-603">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment"></a><span data-ttu-id="1d2e4-604">Detailed tasks for SAP software deployment</span><span class="sxs-lookup"><span data-stu-id="1d2e4-604">Detailed tasks for SAP software deployment</span></span>
<span data-ttu-id="1d2e4-605">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-605">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span></span>

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a><span data-ttu-id="1d2e4-606">Deploy Azure PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="1d2e4-606">Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="1d2e4-607">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-607">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
1.  <span data-ttu-id="1d2e4-608">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-608">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
1.  <span data-ttu-id="1d2e4-609">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-609">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
1.  <span data-ttu-id="1d2e4-610">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-610">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
1.  <span data-ttu-id="1d2e4-611">A page that looks like this appears:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-611">A page that looks like this appears:</span></span>

  <span data-ttu-id="1d2e4-612">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-612">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

1.  <span data-ttu-id="1d2e4-613">Select **Install**, and then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-613">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
1.  <span data-ttu-id="1d2e4-614">PowerShell is installed.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-614">PowerShell is installed.</span></span> <span data-ttu-id="1d2e4-615">Select **Finish** to close the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-615">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="1d2e4-616">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-616">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="1d2e4-617">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-617">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span> <span data-ttu-id="1d2e4-618">The release date and release number of the cmdlets are included on the page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-618">The release date and release number of the cmdlets are included on the page shown in step 5.</span></span> <span data-ttu-id="1d2e4-619">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-619">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="1d2e4-620">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-620">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
(Get-Module AzureRm.Compute).Version
```
<span data-ttu-id="1d2e4-621">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-621">The result looks like this:</span></span>

<span data-ttu-id="1d2e4-622">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-622">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="1d2e4-623">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-623">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span></span> <span data-ttu-id="1d2e4-624">Your PowerShell Azure cmdlets are up-to-date.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-624">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="1d2e4-625">To close the installation wizard, select **Exit**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-625">To close the installation wizard, select **Exit**.</span></span>

<span data-ttu-id="1d2e4-626">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-626">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a><span data-ttu-id="1d2e4-627">Deploy Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1d2e4-627">Deploy Azure CLI</span></span>
1.  <span data-ttu-id="1d2e4-628">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-628">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
1.  <span data-ttu-id="1d2e4-629">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-629">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span></span>
1.  <span data-ttu-id="1d2e4-630">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-630">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
1.  <span data-ttu-id="1d2e4-631">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-631">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
1.  <span data-ttu-id="1d2e4-632">A page that looks like this appears:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-632">A page that looks like this appears:</span></span>

  <span data-ttu-id="1d2e4-633">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-633">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

1.  <span data-ttu-id="1d2e4-634">Select **Install**, and then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-634">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
1.  <span data-ttu-id="1d2e4-635">Azure CLI is installed.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-635">Azure CLI is installed.</span></span> <span data-ttu-id="1d2e4-636">Select **Finish** to close the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-636">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="1d2e4-637">Check frequently for updates to Azure CLI, which usually is updated monthly.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-637">Check frequently for updates to Azure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="1d2e4-638">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-638">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span>

<span data-ttu-id="1d2e4-639">To check the version of Azure CLI that is installed on your computer, run this command:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-639">To check the version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="1d2e4-640">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-640">The result looks like this:</span></span>

<span data-ttu-id="1d2e4-641">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-641">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a><span data-ttu-id="1d2e4-642">Join a VM to an on-premises domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="1d2e4-642">Join a VM to an on-premises domain (Windows only)</span></span>
<span data-ttu-id="1d2e4-643">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-643">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span></span> <span data-ttu-id="1d2e4-644">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-644">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="1d2e4-645">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-645">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="1d2e4-646">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-646">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span></span> <span data-ttu-id="1d2e4-647">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-647">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span></span>

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a><span data-ttu-id="1d2e4-648">Download, install, and enable the Azure VM Agent</span><span class="sxs-lookup"><span data-stu-id="1d2e4-648">Download, install, and enable the Azure VM Agent</span></span>
<span data-ttu-id="1d2e4-649">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-649">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span></span>

<span data-ttu-id="1d2e4-650">If you deploy a VM from the Azure Marketplace, this step is not required.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-650">If you deploy a VM from the Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="1d2e4-651">Images from the Azure Marketplace already have the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-651">Images from the Azure Marketplace already have the Azure VM Agent.</span></span>

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a><span data-ttu-id="1d2e4-652">Windows</span><span class="sxs-lookup"><span data-stu-id="1d2e4-652">Windows</span></span>
1.  <span data-ttu-id="1d2e4-653">Download the Azure VM Agent:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-653">Download the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="1d2e4-654">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-654">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  1.  <span data-ttu-id="1d2e4-655">Store the VM Agent MSI package locally on a personal computer or server.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-655">Store the VM Agent MSI package locally on a personal computer or server.</span></span>
1.  <span data-ttu-id="1d2e4-656">Install the Azure VM Agent:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-656">Install the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="1d2e4-657">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-657">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  1.  <span data-ttu-id="1d2e4-658">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-658">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span></span>
  1.  <span data-ttu-id="1d2e4-659">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-659">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span></span>
  1.  <span data-ttu-id="1d2e4-660">Double-click the MSI file on the VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-660">Double-click the MSI file on the VM.</span></span>
1.  <span data-ttu-id="1d2e4-661">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-661">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="1d2e4-662">The VM Agent runs in this context and needs to be able to connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-662">The VM Agent runs in this context and needs to be able to connect to Azure.</span></span>

<span data-ttu-id="1d2e4-663">No user interaction is required to update the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-663">No user interaction is required to update the Azure VM Agent.</span></span> <span data-ttu-id="1d2e4-664">The VM Agent is automatically updated, and does not require a VM restart.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-664">The VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a><span data-ttu-id="1d2e4-665">Linux</span><span class="sxs-lookup"><span data-stu-id="1d2e4-665">Linux</span></span>
<span data-ttu-id="1d2e4-666">Use the following commands to install the VM Agent for Linux:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-666">Use the following commands to install the VM Agent for Linux:</span></span>

* <span data-ttu-id="1d2e4-667">**SUSE Linux Enterprise Server (SLES)**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-667">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="1d2e4-668">**Red Hat Enterprise Linux (RHEL) or Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-668">**Red Hat Enterprise Linux (RHEL) or Oracle Linux**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="1d2e4-669">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-669">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a><span data-ttu-id="1d2e4-670">Configure the proxy</span><span class="sxs-lookup"><span data-stu-id="1d2e4-670">Configure the proxy</span></span>
<span data-ttu-id="1d2e4-671">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-671">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="1d2e4-672">Windows</span><span class="sxs-lookup"><span data-stu-id="1d2e4-672">Windows</span></span>
<span data-ttu-id="1d2e4-673">Proxy settings must be set up correctly for the Local System account to access the Internet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-673">Proxy settings must be set up correctly for the Local System account to access the Internet.</span></span> <span data-ttu-id="1d2e4-674">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-674">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span></span>

1. <span data-ttu-id="1d2e4-675">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-675">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
1. <span data-ttu-id="1d2e4-676">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-676">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="1d2e4-677">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-677">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
1. <span data-ttu-id="1d2e4-678">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-678">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span></span>
1. <span data-ttu-id="1d2e4-679">On the **Connections** tab, select the **LAN settings** button.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-679">On the **Connections** tab, select the **LAN settings** button.</span></span>
1. <span data-ttu-id="1d2e4-680">Clear the **Automatically detect settings** check box.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-680">Clear the **Automatically detect settings** check box.</span></span>
1. <span data-ttu-id="1d2e4-681">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-681">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span></span>
1. <span data-ttu-id="1d2e4-682">Select the **Advanced** button.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-682">Select the **Advanced** button.</span></span>
1. <span data-ttu-id="1d2e4-683">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-683">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span></span> <span data-ttu-id="1d2e4-684">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-684">Select **OK**.</span></span>

#### <a name="linux"></a><span data-ttu-id="1d2e4-685">Linux</span><span class="sxs-lookup"><span data-stu-id="1d2e4-685">Linux</span></span>
<span data-ttu-id="1d2e4-686">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-686">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="1d2e4-687">Set the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-687">Set the following parameters:</span></span>

1.  <span data-ttu-id="1d2e4-688">**HTTP proxy host**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-688">**HTTP proxy host**.</span></span> <span data-ttu-id="1d2e4-689">For example, set it to **proxy.corp.local**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-689">For example, set it to **proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
1.  <span data-ttu-id="1d2e4-690">**HTTP proxy port**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-690">**HTTP proxy port**.</span></span> <span data-ttu-id="1d2e4-691">For example, set it to **80**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-691">For example, set it to **80**.</span></span>
  ```
  HttpProxy.Port=<port of the proxy host>

  ```
1.  <span data-ttu-id="1d2e4-692">Restart the agent.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-692">Restart the agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="1d2e4-693">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-693">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span></span> <span data-ttu-id="1d2e4-694">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-694">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="1d2e4-695">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-695">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="1d2e4-696">**SLES**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-696">**SLES**</span></span>

  <span data-ttu-id="1d2e4-697">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-697">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="1d2e4-698">The following figure shows an example:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-698">The following figure shows an example:</span></span>

  ![Forced tunneling][deployment-guide-figure-50]


* <span data-ttu-id="1d2e4-700">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-700">**RHEL**</span></span>

  <span data-ttu-id="1d2e4-701">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-701">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="1d2e4-702">For an example, see the preceding figure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-702">For an example, see the preceding figure.</span></span>

* <span data-ttu-id="1d2e4-703">**Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-703">**Oracle Linux**</span></span>

  <span data-ttu-id="1d2e4-704">There are no repositories for Oracle Linux on Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-704">There are no repositories for Oracle Linux on Azure.</span></span> <span data-ttu-id="1d2e4-705">You need to configure your own repositories for Oracle Linux or use the public repositories.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-705">You need to configure your own repositories for Oracle Linux or use the public repositories.</span></span>

<span data-ttu-id="1d2e4-706">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-706">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a><span data-ttu-id="1d2e4-707">Configure the Azure Enhanced Monitoring Extension for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-707">Configure the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="1d2e4-708">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-708">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="1d2e4-709">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-709">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span></span> <span data-ttu-id="1d2e4-710">For more information, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-9.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-710">For more information, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-9.1].</span></span>

<span data-ttu-id="1d2e4-711">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-711">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="1d2e4-712">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-712">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="1d2e4-713">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-713">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a><span data-ttu-id="1d2e4-714">Azure PowerShell for Linux and Windows VMs</span><span class="sxs-lookup"><span data-stu-id="1d2e4-714">Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="1d2e4-715">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-715">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="1d2e4-716">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-716">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span></span> <span data-ttu-id="1d2e4-717">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-717">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
1. <span data-ttu-id="1d2e4-718">Run the following PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-718">Run the following PowerShell cmdlet.</span></span>
    <span data-ttu-id="1d2e4-719">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-719">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="1d2e4-720">If you want to use global Azure, your environment is **AzureCloud**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-720">If you want to use global Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="1d2e4-721">For Azure in China, select **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-721">For Azure in China, select **AzureChinaCloud**.</span></span>

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of the environment>
    Connect-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

<span data-ttu-id="1d2e4-722">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-722">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span></span> <span data-ttu-id="1d2e4-723">This can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-723">This can take several minutes.</span></span>
<span data-ttu-id="1d2e4-724">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-724">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![Successful execution of SAP-specific Azure cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

<span data-ttu-id="1d2e4-726">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-726">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span></span>

<span data-ttu-id="1d2e4-727">The script output includes the following information:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-727">The script output includes the following information:</span></span>

* <span data-ttu-id="1d2e4-728">Confirmation that monitoring for the OS disk and all additional data disks has been configured.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-728">Confirmation that monitoring for the OS disk and all additional data disks has been configured.</span></span>
* <span data-ttu-id="1d2e4-729">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-729">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="1d2e4-730">One line of output gives the status of the actual update of the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-730">One line of output gives the status of the actual update of the monitoring configuration.</span></span>
* <span data-ttu-id="1d2e4-731">Another line of output confirms that the configuration has been deployed or updated.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-731">Another line of output confirms that the configuration has been deployed or updated.</span></span>
* <span data-ttu-id="1d2e4-732">The last line of output is informational.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-732">The last line of output is informational.</span></span> <span data-ttu-id="1d2e4-733">It shows your options for testing the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-733">It shows your options for testing the monitoring configuration.</span></span>
* <span data-ttu-id="1d2e4-734">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-734">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span>
* <span data-ttu-id="1d2e4-735">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-735">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span></span>

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a><span data-ttu-id="1d2e4-736">Azure CLI for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="1d2e4-736">Azure CLI for Linux VMs</span></span>
<span data-ttu-id="1d2e4-737">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-737">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="1d2e4-738">Install using Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d2e4-738">Install using Azure CLI 1.0</span></span>

   1. <span data-ttu-id="1d2e4-739">Install Azure CLI 1.0, as described in [Install the Azure CLI 1.0][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-739">Install Azure CLI 1.0, as described in [Install the Azure CLI 1.0][azure-cli].</span></span>
   1. <span data-ttu-id="1d2e4-740">Sign in with your Azure account:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-740">Sign in with your Azure account:</span></span>

      ```
      azure login
      ```

   1. <span data-ttu-id="1d2e4-741">Switch to Azure Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-741">Switch to Azure Resource Manager mode:</span></span>

      ```
      azure config mode arm
      ```

   1. <span data-ttu-id="1d2e4-742">Enable Azure Enhanced Monitoring:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-742">Enable Azure Enhanced Monitoring:</span></span>

      ```
      azure vm enable-aem <resource-group-name> <vm-name>
      ```

1. <span data-ttu-id="1d2e4-743">Install using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d2e4-743">Install using Azure CLI 2.0</span></span>

   1. <span data-ttu-id="1d2e4-744">Install Azure CLI 2.0, as described in [Install Azure CLI 2.0][azure-cli-2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-744">Install Azure CLI 2.0, as described in [Install Azure CLI 2.0][azure-cli-2].</span></span>
   1. <span data-ttu-id="1d2e4-745">Sign in with your Azure account:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-745">Sign in with your Azure account:</span></span>

      ```
      az login
      ```

   1. <span data-ttu-id="1d2e4-746">Install Azure CLI AEM Extension</span><span class="sxs-lookup"><span data-stu-id="1d2e4-746">Install Azure CLI AEM Extension</span></span>
  
      ```
      az extension add --name aem
      ```
  
   1. <span data-ttu-id="1d2e4-747">Install the extension with</span><span class="sxs-lookup"><span data-stu-id="1d2e4-747">Install the extension with</span></span>
  
      ```
      az vm aem set -g <resource-group-name> -n <vm name>
      ```

1. <span data-ttu-id="1d2e4-748">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-748">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span></span> <span data-ttu-id="1d2e4-749">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-749">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="1d2e4-750">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-750">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span></span>

   ```
   cat /var/lib/AzureEnhancedMonitor/PerfCounters
   ```

   <span data-ttu-id="1d2e4-751">The output looks like this:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-751">The output looks like this:</span></span>
   ```
   ...
   2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
   2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
   ...
   ```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a><span data-ttu-id="1d2e4-752">Checks and troubleshooting for end-to-end monitoring</span><span class="sxs-lookup"><span data-stu-id="1d2e4-752">Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="1d2e4-753">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-753">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="1d2e4-754">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-754">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="1d2e4-755">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring has been set up successfully.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-755">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring has been set up successfully.</span></span> <span data-ttu-id="1d2e4-756">You can proceed with the installation of SAP Host Agent as described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-756">You can proceed with the installation of SAP Host Agent as described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="1d2e4-757">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-757">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="1d2e4-758">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-758">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a><span data-ttu-id="1d2e4-759">Readiness check for the Azure Enhanced Monitoring Extension for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-759">Readiness check for the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="1d2e4-760">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-760">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-the-readiness-check-on-a-windows-vm"></a><span data-ttu-id="1d2e4-761">Run the readiness check on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="1d2e4-761">Run the readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="1d2e4-762">Sign in to the Azure virtual machine (using an admin account is not necessary).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-762">Sign in to the Azure virtual machine (using an admin account is not necessary).</span></span>
1.  <span data-ttu-id="1d2e4-763">Open a Command Prompt window.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-763">Open a Command Prompt window.</span></span>
1.  <span data-ttu-id="1d2e4-764">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span><span class="sxs-lookup"><span data-stu-id="1d2e4-764">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="1d2e4-765">The *version* in the path to the monitoring extension might vary.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-765">The *version* in the path to the monitoring extension might vary.</span></span> <span data-ttu-id="1d2e4-766">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-766">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span></span>

  ![Properties of service running the Azure Enhanced Monitoring Extension for SAP][deployment-guide-figure-1000]

1.  <span data-ttu-id="1d2e4-768">At the command prompt, run **azperflib.exe** without any parameters.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-768">At the command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1d2e4-769">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-769">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span></span> <span data-ttu-id="1d2e4-770">To end the loop, close the Command Prompt window.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-770">To end the loop, close the Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="1d2e4-771">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-771">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span></span> <span data-ttu-id="1d2e4-772">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-772">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-the-output-of-azperflibexe"></a><span data-ttu-id="1d2e4-773">Check the output of azperflib.exe</span><span class="sxs-lookup"><span data-stu-id="1d2e4-773">Check the output of azperflib.exe</span></span>
<span data-ttu-id="1d2e4-774">Azperflib.exe output shows all populated Azure performance counters for SAP.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-774">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="1d2e4-775">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-775">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span></span>

<span data-ttu-id="1d2e4-776">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-776">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="1d2e4-777">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-777">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span></span>

<span data-ttu-id="1d2e4-778">Interpret the resulting values as follows:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-778">Interpret the resulting values as follows:</span></span>

| <span data-ttu-id="1d2e4-779">Azperflib.exe result values</span><span class="sxs-lookup"><span data-stu-id="1d2e4-779">Azperflib.exe result values</span></span> | <span data-ttu-id="1d2e4-780">Azure monitoring health status</span><span class="sxs-lookup"><span data-stu-id="1d2e4-780">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="1d2e4-781">**API Calls - not available**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-781">**API Calls - not available**</span></span> | <span data-ttu-id="1d2e4-782">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-782">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span></span> <span data-ttu-id="1d2e4-783">See **Health status**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-783">See **Health status**.</span></span> |
| <span data-ttu-id="1d2e4-784">**Counters total - empty**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-784">**Counters total - empty**</span></span> |<span data-ttu-id="1d2e4-785">The following two Azure storage counters can be empty:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-785">The following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="1d2e4-786">Storage Read Op Latency Server msec</span><span class="sxs-lookup"><span data-stu-id="1d2e4-786">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="1d2e4-787">Storage Read Op Latency E2E msec</span><span class="sxs-lookup"><span data-stu-id="1d2e4-787">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="1d2e4-788">All other counters must have values.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-788">All other counters must have values.</span></span> |
| <span data-ttu-id="1d2e4-789">**Health status**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-789">**Health status**</span></span> |<span data-ttu-id="1d2e4-790">Only OK if return status shows **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-790">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="1d2e4-791">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-791">**Diagnostics**</span></span> |<span data-ttu-id="1d2e4-792">Detailed information about health status.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-792">Detailed information about health status.</span></span> |

<span data-ttu-id="1d2e4-793">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-793">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-the-readiness-check-on-a-linux-vm"></a><span data-ttu-id="1d2e4-794">Run the readiness check on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="1d2e4-794">Run the readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="1d2e4-795">Connect to the Azure Virtual Machine by using SSH.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-795">Connect to the Azure Virtual Machine by using SSH.</span></span>

1.  <span data-ttu-id="1d2e4-796">Check the output of the Azure Enhanced Monitoring Extension.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-796">Check the output of the Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="1d2e4-797">a.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-797">a.</span></span>  <span data-ttu-id="1d2e4-798">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-798">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="1d2e4-799">**Expected result**: Returns list of performance counters.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-799">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="1d2e4-800">The file should not be empty.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-800">The file should not be empty.</span></span>

 <span data-ttu-id="1d2e4-801">b.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-801">b.</span></span> <span data-ttu-id="1d2e4-802">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-802">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="1d2e4-803">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span><span class="sxs-lookup"><span data-stu-id="1d2e4-803">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="1d2e4-804">c.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-804">c.</span></span> <span data-ttu-id="1d2e4-805">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-805">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="1d2e4-806">**Expected result**: Returns as empty or does not exist.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-806">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="1d2e4-807">If the preceding check was not successful, run these additional checks:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-807">If the preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="1d2e4-808">Make sure that the waagent is installed and enabled.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-808">Make sure that the waagent is installed and enabled.</span></span>

  <span data-ttu-id="1d2e4-809">a.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-809">a.</span></span>  <span data-ttu-id="1d2e4-810">Run `sudo ls -al /var/lib/waagent/`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-810">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="1d2e4-811">**Expected result**: Lists the content of the waagent directory.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-811">**Expected result**: Lists the content of the waagent directory.</span></span>

  <span data-ttu-id="1d2e4-812">b.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-812">b.</span></span>  <span data-ttu-id="1d2e4-813">Run `ps -ax | grep waagent`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-813">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="1d2e4-814">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-814">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

1.   <span data-ttu-id="1d2e4-815">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-815">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="1d2e4-816">a.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-816">a.</span></span>  <span data-ttu-id="1d2e4-817">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-817">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`</span></span>

    <span data-ttu-id="1d2e4-818">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-818">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="1d2e4-819">b.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-819">b.</span></span> <span data-ttu-id="1d2e4-820">Run `ps -ax | grep AzureEnhanced`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-820">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="1d2e4-821">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-821">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

1. <span data-ttu-id="1d2e4-822">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-822">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span></span>

  <span data-ttu-id="1d2e4-823">a.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-823">a.</span></span>  <span data-ttu-id="1d2e4-824">Run `/usr/sap/hostctrl/exe/saposcol -d`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-824">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="1d2e4-825">b.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-825">b.</span></span>  <span data-ttu-id="1d2e4-826">Run `dump ccm`</span><span class="sxs-lookup"><span data-stu-id="1d2e4-826">Run `dump ccm`</span></span>

  <span data-ttu-id="1d2e4-827">c.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-827">c.</span></span>  <span data-ttu-id="1d2e4-828">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-828">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="1d2e4-829">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-829">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="1d2e4-830">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-830">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a><span data-ttu-id="1d2e4-831">Health check for the Azure monitoring infrastructure configuration</span><span class="sxs-lookup"><span data-stu-id="1d2e4-831">Health check for the Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="1d2e4-832">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-832">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="1d2e4-833">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-833">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
1.  <span data-ttu-id="1d2e4-834">Run the following PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-834">Run the following PowerShell cmdlet.</span></span> <span data-ttu-id="1d2e4-835">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-835">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="1d2e4-836">To use global Azure, select the **AzureCloud** environment.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-836">To use global Azure, select the **AzureCloud** environment.</span></span> <span data-ttu-id="1d2e4-837">For Azure in China, select **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-837">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of the environment>
  Connect-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

1.  <span data-ttu-id="1d2e4-838">Enter your account data and identify the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-838">Enter your account data and identify the Azure virtual machine.</span></span>

  ![Input page of SAP-specific Azure cmdlet Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

1. <span data-ttu-id="1d2e4-840">The script tests the configuration of the virtual machine you select.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-840">The script tests the configuration of the virtual machine you select.</span></span>

  ![Output of successful test of the Azure monitoring infrastructure for SAP][deployment-guide-figure-1300]

<span data-ttu-id="1d2e4-842">Make sure that every health check result is **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-842">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="1d2e4-843">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-843">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1d2e4-844">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-844">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="1d2e4-845">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-845">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a><span data-ttu-id="1d2e4-846">Troubleshooting the Azure monitoring infrastructure for SAP</span><span class="sxs-lookup"><span data-stu-id="1d2e4-846">Troubleshooting the Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="1d2e4-848">Azure performance counters do not show up at all</span><span class="sxs-lookup"><span data-stu-id="1d2e4-848">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="1d2e4-849">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-849">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="1d2e4-850">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-850">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="1d2e4-851">The installation directory of the Azure Enhanced Monitoring Extension is empty</span><span class="sxs-lookup"><span data-stu-id="1d2e4-851">The installation directory of the Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="1d2e4-852">Issue</span><span class="sxs-lookup"><span data-stu-id="1d2e4-852">Issue</span></span>
<span data-ttu-id="1d2e4-853">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-853">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="1d2e4-854">Solution</span><span class="sxs-lookup"><span data-stu-id="1d2e4-854">Solution</span></span>
<span data-ttu-id="1d2e4-855">The extension is not installed.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-855">The extension is not installed.</span></span> <span data-ttu-id="1d2e4-856">Determine whether this is a proxy issue (as described earlier).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-856">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="1d2e4-857">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-857">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="1d2e4-858">Service for Azure Enhanced Monitoring does not exist</span><span class="sxs-lookup"><span data-stu-id="1d2e4-858">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="1d2e4-859">Issue</span><span class="sxs-lookup"><span data-stu-id="1d2e4-859">Issue</span></span>
<span data-ttu-id="1d2e4-860">The AzureEnhancedMonitoring Windows service does not exist.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-860">The AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="1d2e4-861">Azperflib.exe output throws an error:</span><span class="sxs-lookup"><span data-stu-id="1d2e4-861">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="1d2e4-862">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="1d2e4-862">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="1d2e4-863">Solution</span><span class="sxs-lookup"><span data-stu-id="1d2e4-863">Solution</span></span>
<span data-ttu-id="1d2e4-864">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-864">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="1d2e4-865">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-865">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="1d2e4-866">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-866">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-to-start"></a><span data-ttu-id="1d2e4-867">Service for Azure Enhanced Monitoring exists, but fails to start</span><span class="sxs-lookup"><span data-stu-id="1d2e4-867">Service for Azure Enhanced Monitoring exists, but fails to start</span></span>

###### <a name="issue"></a><span data-ttu-id="1d2e4-868">Issue</span><span class="sxs-lookup"><span data-stu-id="1d2e4-868">Issue</span></span>
<span data-ttu-id="1d2e4-869">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-869">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span></span> <span data-ttu-id="1d2e4-870">For more information, check the application event log.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-870">For more information, check the application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="1d2e4-871">Solution</span><span class="sxs-lookup"><span data-stu-id="1d2e4-871">Solution</span></span>
<span data-ttu-id="1d2e4-872">The configuration is incorrect.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-872">The configuration is incorrect.</span></span> <span data-ttu-id="1d2e4-873">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-873">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="1d2e4-875">Some Azure performance counters are missing</span><span class="sxs-lookup"><span data-stu-id="1d2e4-875">Some Azure performance counters are missing</span></span>
<span data-ttu-id="1d2e4-876">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-876">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="1d2e4-877">The service gets data from several sources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-877">The service gets data from several sources.</span></span> <span data-ttu-id="1d2e4-878">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-878">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="1d2e4-879">Storage counters are used from your logging on the storage subscription level.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-879">Storage counters are used from your logging on the storage subscription level.</span></span>

<span data-ttu-id="1d2e4-880">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-880">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="1d2e4-881">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-881">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="1d2e4-882">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-882">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="1d2e4-884">Azure performance counters do not show up at all</span><span class="sxs-lookup"><span data-stu-id="1d2e4-884">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="1d2e4-885">Performance metrics in Azure are collected by a daemon.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-885">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="1d2e4-886">If the daemon is not running, no performance metrics can be collected.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-886">If the daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="1d2e4-887">The installation directory of the Azure Enhanced Monitoring extension is empty</span><span class="sxs-lookup"><span data-stu-id="1d2e4-887">The installation directory of the Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="1d2e4-888">Issue</span><span class="sxs-lookup"><span data-stu-id="1d2e4-888">Issue</span></span>
<span data-ttu-id="1d2e4-889">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-889">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="1d2e4-890">Solution</span><span class="sxs-lookup"><span data-stu-id="1d2e4-890">Solution</span></span>
<span data-ttu-id="1d2e4-891">The extension is not installed.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-891">The extension is not installed.</span></span> <span data-ttu-id="1d2e4-892">Determine whether this is a proxy issue (as described earlier).</span><span class="sxs-lookup"><span data-stu-id="1d2e4-892">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="1d2e4-893">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-893">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="1d2e4-895">Some Azure performance counters are missing</span><span class="sxs-lookup"><span data-stu-id="1d2e4-895">Some Azure performance counters are missing</span></span>
<span data-ttu-id="1d2e4-896">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-896">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="1d2e4-897">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-897">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="1d2e4-898">Storage counters come from the logs in your storage subscription.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-898">Storage counters come from the logs in your storage subscription.</span></span>

<span data-ttu-id="1d2e4-899">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-899">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="1d2e4-900">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="1d2e4-900">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="1d2e4-901">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-901">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="1d2e4-902">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d2e4-902">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
