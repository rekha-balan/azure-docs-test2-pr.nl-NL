---
title: Azure Virtual Machines deployment for SAP on Linux | Microsoft Docs
description: Learn how to deploy SAP software on Linux virtual machines in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: MSSedusch
manager: timlt
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
ms.openlocfilehash: 11996c9daac666493f8d5b11027c7cc928154f6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550249"
---
# <a name="azure-virtual-machines-deployment-for-sap"></a><span data-ttu-id="afa81-103">Azure Virtual Machines deployment for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-103">Azure Virtual Machines deployment for SAP</span></span>
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

[azure-cli]:../../../cli-install-nodejs.md
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

[dbms-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

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
[deployment-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
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

[Logo_Linux]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

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

[planning-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/storage-premium-storage.md
[storage-redundancy]:../../../storage/storage-redundancy.md
[storage-scalability-targets]:../../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
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

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="afa81-183">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span><span class="sxs-lookup"><span data-stu-id="afa81-183">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="afa81-184">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-184">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="afa81-185">Extend an application's reliability and availability without additional on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="afa81-185">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="afa81-186">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span><span class="sxs-lookup"><span data-stu-id="afa81-186">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="afa81-187">In this article, we cover the steps to deploy SAP applications on Linux virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="afa81-187">In this article, we cover the steps to deploy SAP applications on Linux virtual machines (VMs) in Azure, including alternate deployment options and troubleshooting.</span></span> <span data-ttu-id="afa81-188">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-188">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span> <span data-ttu-id="afa81-189">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span><span class="sxs-lookup"><span data-stu-id="afa81-189">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa81-190">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="afa81-190">Prerequisites</span></span>
<span data-ttu-id="afa81-191">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span><span class="sxs-lookup"><span data-stu-id="afa81-191">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="afa81-192">Before you start, make sure that you meet the prerequisites for installing SAP software on Linux virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-192">Before you start, make sure that you meet the prerequisites for installing SAP software on Linux virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="afa81-193">Local computer</span><span class="sxs-lookup"><span data-stu-id="afa81-193">Local computer</span></span>
<span data-ttu-id="afa81-194">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="afa81-194">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span></span> <span data-ttu-id="afa81-195">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span><span class="sxs-lookup"><span data-stu-id="afa81-195">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="afa81-196">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="afa81-196">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="afa81-197">Internet connection</span><span class="sxs-lookup"><span data-stu-id="afa81-197">Internet connection</span></span>
<span data-ttu-id="afa81-198">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="afa81-198">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span></span> <span data-ttu-id="afa81-199">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="afa81-199">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span></span> <span data-ttu-id="afa81-200">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="afa81-200">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="afa81-201">Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="afa81-201">Microsoft Azure subscription</span></span>
<span data-ttu-id="afa81-202">You need an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="afa81-202">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="afa81-203">Topology and networking</span><span class="sxs-lookup"><span data-stu-id="afa81-203">Topology and networking</span></span>
<span data-ttu-id="afa81-204">You need to define the topology and architecture of the SAP deployment in Azure:</span><span class="sxs-lookup"><span data-stu-id="afa81-204">You need to define the topology and architecture of the SAP deployment in Azure:</span></span>

* <span data-ttu-id="afa81-205">Azure storage accounts to be used</span><span class="sxs-lookup"><span data-stu-id="afa81-205">Azure storage accounts to be used</span></span>
* <span data-ttu-id="afa81-206">Virtual network where you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="afa81-206">Virtual network where you want to deploy the SAP system</span></span>
* <span data-ttu-id="afa81-207">Resource group to which you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="afa81-207">Resource group to which you want to deploy the SAP system</span></span>
* <span data-ttu-id="afa81-208">Azure region where you want to deploy the SAP system</span><span class="sxs-lookup"><span data-stu-id="afa81-208">Azure region where you want to deploy the SAP system</span></span>
* <span data-ttu-id="afa81-209">SAP configuration (two-tier or three-tier)</span><span class="sxs-lookup"><span data-stu-id="afa81-209">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="afa81-210">VM sizes and the number of additional virtual hard disks (VHDs) to be mounted to the VMs</span><span class="sxs-lookup"><span data-stu-id="afa81-210">VM sizes and the number of additional virtual hard disks (VHDs) to be mounted to the VMs</span></span>
* <span data-ttu-id="afa81-211">SAP Correction and Transport System (CTS) configuration</span><span class="sxs-lookup"><span data-stu-id="afa81-211">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="afa81-212">Create and configure Azure storage accounts or Azure virtual networks before you begin the SAP software deployment process.</span><span class="sxs-lookup"><span data-stu-id="afa81-212">Create and configure Azure storage accounts or Azure virtual networks before you begin the SAP software deployment process.</span></span> <span data-ttu-id="afa81-213">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-213">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="afa81-214">SAP sizing</span><span class="sxs-lookup"><span data-stu-id="afa81-214">SAP sizing</span></span>
<span data-ttu-id="afa81-215">Know the following information, for SAP sizing:</span><span class="sxs-lookup"><span data-stu-id="afa81-215">Know the following information, for SAP sizing:</span></span>

* <span data-ttu-id="afa81-216">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span><span class="sxs-lookup"><span data-stu-id="afa81-216">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="afa81-217">Required CPU resource and memory consumption of the SAP system</span><span class="sxs-lookup"><span data-stu-id="afa81-217">Required CPU resource and memory consumption of the SAP system</span></span>
* <span data-ttu-id="afa81-218">Required input/output (I/O) operations per second</span><span class="sxs-lookup"><span data-stu-id="afa81-218">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="afa81-219">Required network bandwidth of eventual communication between VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="afa81-219">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="afa81-220">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span><span class="sxs-lookup"><span data-stu-id="afa81-220">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="afa81-221">Resource groups</span><span class="sxs-lookup"><span data-stu-id="afa81-221">Resource groups</span></span>
<span data-ttu-id="afa81-222">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="afa81-222">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="afa81-223">For more information, see [Azure Resource Manager overview][resource-group-overview].</span><span class="sxs-lookup"><span data-stu-id="afa81-223">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="afa81-224">Resources</span><span class="sxs-lookup"><span data-stu-id="afa81-224">Resources</span></span>

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a><span data-ttu-id="afa81-225">SAP resources</span><span class="sxs-lookup"><span data-stu-id="afa81-225">SAP resources</span></span>
<span data-ttu-id="afa81-226">When you are setting up your SAP software deployment, you need the following SAP resources:</span><span class="sxs-lookup"><span data-stu-id="afa81-226">When you are setting up your SAP software deployment, you need the following SAP resources:</span></span>

* <span data-ttu-id="afa81-227">SAP Note [1928533], which has:</span><span class="sxs-lookup"><span data-stu-id="afa81-227">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="afa81-228">List of Azure VM sizes that are supported for the deployment of SAP software</span><span class="sxs-lookup"><span data-stu-id="afa81-228">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="afa81-229">Important capacity information for Azure VM sizes</span><span class="sxs-lookup"><span data-stu-id="afa81-229">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="afa81-230">Supported SAP software, and operating system (OS) and database combinations</span><span class="sxs-lookup"><span data-stu-id="afa81-230">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="afa81-231">Required SAP kernel version for Windows and Linux on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="afa81-231">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="afa81-232">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-232">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="afa81-233">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-233">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="afa81-234">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-234">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="afa81-235">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-235">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="afa81-236">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-236">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="afa81-237">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="afa81-237">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="afa81-238">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span><span class="sxs-lookup"><span data-stu-id="afa81-238">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="afa81-239">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span><span class="sxs-lookup"><span data-stu-id="afa81-239">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="afa81-240">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span><span class="sxs-lookup"><span data-stu-id="afa81-240">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="afa81-241">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span><span class="sxs-lookup"><span data-stu-id="afa81-241">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="afa81-242">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="afa81-242">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

[comment]: <> (MSSedusch TODO Add ARM patch level for SAP Host Agent in SAP Note 1409604)

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a><span data-ttu-id="afa81-244">Windows resources</span><span class="sxs-lookup"><span data-stu-id="afa81-244">Windows resources</span></span>
<span data-ttu-id="afa81-245">These Microsoft articles cover SAP deployments in Azure:</span><span class="sxs-lookup"><span data-stu-id="afa81-245">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="afa81-246">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-246">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="afa81-247">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-247">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="afa81-248">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-248">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="afa81-249">[Azure portal][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="afa81-249">[Azure portal][azure-portal]</span></span>

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a><span data-ttu-id="afa81-250">Deployment scenarios for SAP software on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="afa81-250">Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="afa81-251">You have multiple options for deploying VMs and associated disks in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-251">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="afa81-252">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span><span class="sxs-lookup"><span data-stu-id="afa81-252">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span></span>

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a><span data-ttu-id="afa81-253">Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-253">Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span></span>
<span data-ttu-id="afa81-254">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-254">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span></span> <span data-ttu-id="afa81-255">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span><span class="sxs-lookup"><span data-stu-id="afa81-255">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="afa81-256">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afa81-256">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="afa81-257">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-257">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>

<span data-ttu-id="afa81-258">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="afa81-258">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM image from the Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="afa81-260">Create a virtual machine by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="afa81-260">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="afa81-261">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="afa81-261">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span></span>

1.  <span data-ttu-id="afa81-262">Go to <https://portal.azure.com/#create>.</span><span class="sxs-lookup"><span data-stu-id="afa81-262">Go to <https://portal.azure.com/#create>.</span></span>  <span data-ttu-id="afa81-263">Or, in the Azure portal menu, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="afa81-263">Or, in the Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="afa81-264">Select **Compute**, and then select the type of operating system you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="afa81-264">Select **Compute**, and then select the type of operating system you want to deploy.</span></span> <span data-ttu-id="afa81-265">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span><span class="sxs-lookup"><span data-stu-id="afa81-265">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span> <span data-ttu-id="afa81-266">The default list view does not show all supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="afa81-266">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="afa81-267">Select **see all** for a full list.</span><span class="sxs-lookup"><span data-stu-id="afa81-267">Select **see all** for a full list.</span></span> <span data-ttu-id="afa81-268">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="afa81-268">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="afa81-269">On the next page, review terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="afa81-269">On the next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="afa81-270">In the **Select a deployment model** box, select **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="afa81-270">In the **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="afa81-271">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="afa81-271">Select **Create**.</span></span>

<span data-ttu-id="afa81-272">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="afa81-272">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="afa81-273">Some of these parameters are:</span><span class="sxs-lookup"><span data-stu-id="afa81-273">Some of these parameters are:</span></span>

1. <span data-ttu-id="afa81-274">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="afa81-274">**Basics**:</span></span>
  * <span data-ttu-id="afa81-275">**Name**: The name of the resource (the virtual machine name).</span><span class="sxs-lookup"><span data-stu-id="afa81-275">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="afa81-276">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span><span class="sxs-lookup"><span data-stu-id="afa81-276">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="afa81-277">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-277">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="afa81-278">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-278">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="afa81-279">**Resource group**: The name of the resource group for the VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-279">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="afa81-280">You can enter either the name of a new resource group or the name of a resource group that already exists.</span><span class="sxs-lookup"><span data-stu-id="afa81-280">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="afa81-281">**Location**: Where to deploy the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-281">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="afa81-282">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="afa81-282">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="afa81-283">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-283">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>
2. <span data-ttu-id="afa81-284">**Size**:</span><span class="sxs-lookup"><span data-stu-id="afa81-284">**Size**:</span></span>

     <span data-ttu-id="afa81-285">For a list of supported VM types, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="afa81-285">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="afa81-286">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="afa81-286">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="afa81-287">Not all VM types support Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="afa81-287">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="afa81-288">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-288">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>

3. <span data-ttu-id="afa81-289">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="afa81-289">**Settings**:</span></span>
   * <span data-ttu-id="afa81-290">**Storage account**: Select an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="afa81-290">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="afa81-291">Not all storage types work for running SAP applications.</span><span class="sxs-lookup"><span data-stu-id="afa81-291">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="afa81-292">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-292">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>
   * <span data-ttu-id="afa81-293">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="afa81-293">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
   * <span data-ttu-id="afa81-294">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span><span class="sxs-lookup"><span data-stu-id="afa81-294">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="afa81-295">You can use a public IP address to access your virtual machine over the Internet.</span><span class="sxs-lookup"><span data-stu-id="afa81-295">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="afa81-296">Make sure that you also create a network security group to help secure access to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-296">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
   * <span data-ttu-id="afa81-297">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span><span class="sxs-lookup"><span data-stu-id="afa81-297">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
   * <span data-ttu-id="afa81-298">**Availability**: Select an availability set, or enter the parameters to create a new availability set.</span><span class="sxs-lookup"><span data-stu-id="afa81-298">**Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="afa81-299">For more information, see [Azure availability sets][planning-guide-3.2.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-299">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
   * <span data-ttu-id="afa81-300">**Monitoring**: You can select **Disable** for monitoring diagnostics.</span><span class="sxs-lookup"><span data-stu-id="afa81-300">**Monitoring**: You can select **Disable** for monitoring diagnostics.</span></span> <span data-ttu-id="afa81-301">It is enabled automatically when you run the commands to enable the Azure Enhanced Monitoring Extension, as described in [Configure monitoring][deployment-guide-configure-monitoring-scenario-1].</span><span class="sxs-lookup"><span data-stu-id="afa81-301">It is enabled automatically when you run the commands to enable the Azure Enhanced Monitoring Extension, as described in [Configure monitoring][deployment-guide-configure-monitoring-scenario-1].</span></span>

4. <span data-ttu-id="afa81-302">**Summary**:</span><span class="sxs-lookup"><span data-stu-id="afa81-302">**Summary**:</span></span>

  <span data-ttu-id="afa81-303">Review your selections, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="afa81-303">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="afa81-304">Your virtual machine is deployed in the resource group you selected.</span><span class="sxs-lookup"><span data-stu-id="afa81-304">Your virtual machine is deployed in the resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="afa81-305">Create a virtual machine by using a template</span><span class="sxs-lookup"><span data-stu-id="afa81-305">Create a virtual machine by using a template</span></span>
<span data-ttu-id="afa81-306">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="afa81-306">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="afa81-307">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span><span class="sxs-lookup"><span data-stu-id="afa81-307">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="afa81-308">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="afa81-308">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="afa81-309">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="afa81-309">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="afa81-310">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="afa81-310">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="afa81-311">To create a three-tier system by using multiple virtual machines, use this template.</span><span class="sxs-lookup"><span data-stu-id="afa81-311">To create a three-tier system by using multiple virtual machines, use this template.</span></span>

<span data-ttu-id="afa81-312">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="afa81-312">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="afa81-313">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="afa81-313">**Basics**:</span></span>
  * <span data-ttu-id="afa81-314">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-314">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="afa81-315">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-315">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="afa81-316">You can create a new resource group, or you can select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="afa81-316">You can create a new resource group, or you can select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="afa81-317">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-317">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="afa81-318">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-318">If you selected an existing resource group, the location of that resource group is used.</span></span>

2. <span data-ttu-id="afa81-319">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="afa81-319">**Settings**:</span></span>
  * <span data-ttu-id="afa81-320">**SAP System ID**: The SAP System ID (SID).</span><span class="sxs-lookup"><span data-stu-id="afa81-320">**SAP System ID**: The SAP System ID (SID).</span></span>
  * <span data-ttu-id="afa81-321">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span><span class="sxs-lookup"><span data-stu-id="afa81-321">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span>

    <span data-ttu-id="afa81-322">The default list view does not show all supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="afa81-322">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="afa81-323">Select **see all** for a full list.</span><span class="sxs-lookup"><span data-stu-id="afa81-323">Select **see all** for a full list.</span></span> <span data-ttu-id="afa81-324">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span><span class="sxs-lookup"><span data-stu-id="afa81-324">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="afa81-325">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="afa81-325">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="afa81-326">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="afa81-326">The number of SAPS the new system provides.</span></span> <span data-ttu-id="afa81-327">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="afa81-327">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="afa81-328">**System availability** (three-tier template only): The system availability.</span><span class="sxs-lookup"><span data-stu-id="afa81-328">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="afa81-329">Select **HA** for a configuration that is suitable for a high-availability installation.</span><span class="sxs-lookup"><span data-stu-id="afa81-329">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="afa81-330">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span><span class="sxs-lookup"><span data-stu-id="afa81-330">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="afa81-331">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="afa81-331">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="afa81-332">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="afa81-332">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="afa81-333">For more information about storage types, see these resources:</span><span class="sxs-lookup"><span data-stu-id="afa81-333">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="afa81-334">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="afa81-334">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="afa81-335">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-335">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="afa81-336">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="afa81-336">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="afa81-337">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="afa81-337">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="afa81-338">**Admin username** and **Admin password**: A username and password.</span><span class="sxs-lookup"><span data-stu-id="afa81-338">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="afa81-339">A new user is created, for signing in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-339">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="afa81-340">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-340">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="afa81-341">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="afa81-341">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="afa81-342">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="afa81-342">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span></span> <span data-ttu-id="afa81-343">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="afa81-343">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="afa81-344">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="afa81-344">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="afa81-345">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="afa81-345">**Terms and conditions**:</span></span>  
    <span data-ttu-id="afa81-346">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="afa81-346">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="afa81-347">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="afa81-347">Select **Purchase**.</span></span>

<span data-ttu-id="afa81-348">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="afa81-348">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="afa81-349">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="afa81-349">Configure proxy settings</span></span>
<span data-ttu-id="afa81-350">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-350">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="afa81-351">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="afa81-351">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="afa81-352">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="afa81-352">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="afa81-353">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="afa81-353">Join a domain (Windows only)</span></span>
<span data-ttu-id="afa81-354">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="afa81-354">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="afa81-355">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-355">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a><span data-ttu-id="afa81-356">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="afa81-356">Configure monitoring</span></span>
<span data-ttu-id="afa81-357">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-357">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="afa81-358">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-358">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="afa81-359">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="afa81-359">Monitoring check</span></span>
<span data-ttu-id="afa81-360">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="afa81-360">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="afa81-361">Post-deployment steps</span><span class="sxs-lookup"><span data-stu-id="afa81-361">Post-deployment steps</span></span>
<span data-ttu-id="afa81-362">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-362">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span></span> <span data-ttu-id="afa81-363">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span><span class="sxs-lookup"><span data-stu-id="afa81-363">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="afa81-364">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span><span class="sxs-lookup"><span data-stu-id="afa81-364">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="afa81-365">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="afa81-365">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="afa81-366">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span><span class="sxs-lookup"><span data-stu-id="afa81-366">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span></span>

[comment]: <> (MSSedusch TODO why do we need to recommend a file management, for example, File Server or VHD? Is that so different from on-premises?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a><span data-ttu-id="afa81-368">Scenario 2: Deploying a VM with a custom image for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-368">Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="afa81-369">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span><span class="sxs-lookup"><span data-stu-id="afa81-369">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="afa81-370">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span><span class="sxs-lookup"><span data-stu-id="afa81-370">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="afa81-371">You use different steps to create a private image for Linux than to create one for Windows.</span><span class="sxs-lookup"><span data-stu-id="afa81-371">You use different steps to create a private image for Linux than to create one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="afa81-373">Windows</span><span class="sxs-lookup"><span data-stu-id="afa81-373">Windows</span></span>
>
> <span data-ttu-id="afa81-374">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-374">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="afa81-375">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span><span class="sxs-lookup"><span data-stu-id="afa81-375">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="afa81-377">Linux</span><span class="sxs-lookup"><span data-stu-id="afa81-377">Linux</span></span>
>
> <span data-ttu-id="afa81-378">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-378">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="afa81-379">You can use `waagent -deprovision`  to do this.</span><span class="sxs-lookup"><span data-stu-id="afa81-379">You can use `waagent -deprovision`  to do this.</span></span> <span data-ttu-id="afa81-380">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span><span class="sxs-lookup"><span data-stu-id="afa81-380">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="afa81-381">You can prepare and create a custom image, and then use it to create multiple new VMs.</span><span class="sxs-lookup"><span data-stu-id="afa81-381">You can prepare and create a custom image, and then use it to create multiple new VMs.</span></span> <span data-ttu-id="afa81-382">This is described in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-382">This is described in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span> <span data-ttu-id="afa81-383">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a VHD that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span><span class="sxs-lookup"><span data-stu-id="afa81-383">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a VHD that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="afa81-384">For more information, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span><span class="sxs-lookup"><span data-stu-id="afa81-384">For more information, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span> <span data-ttu-id="afa81-385">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span><span class="sxs-lookup"><span data-stu-id="afa81-385">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="afa81-386">Otherwise, you can install the SAP software after you deploy the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-386">Otherwise, you can install the SAP software after you deploy the Azure VM.</span></span>

<span data-ttu-id="afa81-387">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span><span class="sxs-lookup"><span data-stu-id="afa81-387">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM image in private Marketplace][deployment-guide-figure-300]

#### <a name="create-the-virtual-machine"></a><span data-ttu-id="afa81-389">Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="afa81-389">Create the virtual machine</span></span>
<span data-ttu-id="afa81-390">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span><span class="sxs-lookup"><span data-stu-id="afa81-390">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span></span> <span data-ttu-id="afa81-391">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="afa81-391">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="afa81-392">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="afa81-392">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="afa81-393">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="afa81-393">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="afa81-394">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="afa81-394">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="afa81-395">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="afa81-395">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="afa81-396">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span><span class="sxs-lookup"><span data-stu-id="afa81-396">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>

<span data-ttu-id="afa81-397">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="afa81-397">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="afa81-398">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="afa81-398">**Basics**:</span></span>
  * <span data-ttu-id="afa81-399">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-399">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="afa81-400">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-400">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="afa81-401">You can create a new resource group or select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="afa81-401">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="afa81-402">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-402">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="afa81-403">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-403">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="afa81-404">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="afa81-404">**Settings**:</span></span>
  * <span data-ttu-id="afa81-405">**SAP System ID**: The SAP System ID.</span><span class="sxs-lookup"><span data-stu-id="afa81-405">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="afa81-406">**OS type**: The operating system type you want to deploy (Windows or Linux).</span><span class="sxs-lookup"><span data-stu-id="afa81-406">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="afa81-407">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="afa81-407">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="afa81-408">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="afa81-408">The number of SAPS the new system provides.</span></span> <span data-ttu-id="afa81-409">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="afa81-409">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="afa81-410">**System availability** (three-tier template only): The system availability.</span><span class="sxs-lookup"><span data-stu-id="afa81-410">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="afa81-411">Select **HA** for a configuration that is suitable for a high-availability installation.</span><span class="sxs-lookup"><span data-stu-id="afa81-411">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="afa81-412">Two database servers and two servers for ASCS are created.</span><span class="sxs-lookup"><span data-stu-id="afa81-412">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="afa81-413">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="afa81-413">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="afa81-414">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="afa81-414">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="afa81-415">For more information about storage types, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="afa81-415">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="afa81-416">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="afa81-416">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="afa81-417">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-417">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="afa81-418">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="afa81-418">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="afa81-419">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="afa81-419">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="afa81-420">**User image VHD URI**: The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="afa81-420">**User image VHD URI**: The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="afa81-421">**User image storage account**: The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span><span class="sxs-lookup"><span data-stu-id="afa81-421">**User image storage account**: The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="afa81-422">**Admin username** and **Admin password**: The username and password.</span><span class="sxs-lookup"><span data-stu-id="afa81-422">**Admin username** and **Admin password**: The username and password.</span></span>

    <span data-ttu-id="afa81-423">A new user is created, for signing in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-423">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="afa81-424">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-424">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="afa81-425">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="afa81-425">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="afa81-426">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="afa81-426">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="afa81-427">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="afa81-427">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="afa81-428">The ID usually looks like this:</span><span class="sxs-lookup"><span data-stu-id="afa81-428">The ID usually looks like this:</span></span>

    <span data-ttu-id="afa81-429">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="afa81-429">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="afa81-430">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="afa81-430">**Terms and conditions**:</span></span>  
    <span data-ttu-id="afa81-431">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="afa81-431">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="afa81-432">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="afa81-432">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent-linux-only"></a><span data-ttu-id="afa81-433">Install the VM Agent (Linux only)</span><span class="sxs-lookup"><span data-stu-id="afa81-433">Install the VM Agent (Linux only)</span></span>
<span data-ttu-id="afa81-434">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="afa81-434">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span></span> <span data-ttu-id="afa81-435">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="afa81-435">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="afa81-436">If you don’t use the templates, you also can install the VM Agent later.</span><span class="sxs-lookup"><span data-stu-id="afa81-436">If you don’t use the templates, you also can install the VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="afa81-437">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="afa81-437">Join a domain (Windows only)</span></span>
<span data-ttu-id="afa81-438">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="afa81-438">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="afa81-439">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-439">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="afa81-440">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="afa81-440">Configure proxy settings</span></span>
<span data-ttu-id="afa81-441">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-441">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="afa81-442">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="afa81-442">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="afa81-443">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="afa81-443">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="afa81-444">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="afa81-444">Configure monitoring</span></span>
<span data-ttu-id="afa81-445">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-445">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="afa81-446">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-446">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="afa81-447">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="afa81-447">Monitoring check</span></span>
<span data-ttu-id="afa81-448">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="afa81-448">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a><span data-ttu-id="afa81-449">Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-449">Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="afa81-450">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-450">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span></span> <span data-ttu-id="afa81-451">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-451">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span></span> <span data-ttu-id="afa81-452">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="afa81-452">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span></span> <span data-ttu-id="afa81-453">You do not need to generalize the OS.</span><span class="sxs-lookup"><span data-stu-id="afa81-453">You do not need to generalize the OS.</span></span> <span data-ttu-id="afa81-454">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-454">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="afa81-455">In this scenario, the VM Agent is not automatically installed during deployment.</span><span class="sxs-lookup"><span data-stu-id="afa81-455">In this scenario, the VM Agent is not automatically installed during deployment.</span></span> <span data-ttu-id="afa81-456">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP required for to run SAP, you need to download, install, and enable both components manually after you create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-456">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP required for to run SAP, you need to download, install, and enable both components manually after you create the virtual machine.</span></span>

<span data-ttu-id="afa81-457">For more information about the Azure VM Agent, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="afa81-457">For more information about the Azure VM Agent, see the following resources.</span></span>

[comment]: <> (MSSedusch TODO Update Windows Link below)

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="afa81-460">Windows</span><span class="sxs-lookup"><span data-stu-id="afa81-460">Windows</span></span>
>
> <http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx>
>
> ![Linux][Logo_Linux] <span data-ttu-id="afa81-462">Linux</span><span class="sxs-lookup"><span data-stu-id="afa81-462">Linux</span></span>
>
> <span data-ttu-id="afa81-463">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-463">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="afa81-464">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span><span class="sxs-lookup"><span data-stu-id="afa81-464">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![Flowchart of VM deployment for SAP systems by using a VM disk][deployment-guide-figure-400]

<span data-ttu-id="afa81-466">Assuming that the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), do the tasks described in the next few sections.</span><span class="sxs-lookup"><span data-stu-id="afa81-466">Assuming that the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), do the tasks described in the next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="afa81-467">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="afa81-467">Create a virtual machine</span></span>
<span data-ttu-id="afa81-468">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span><span class="sxs-lookup"><span data-stu-id="afa81-468">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="afa81-469">You also can manually create a virtual machine, by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afa81-469">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="afa81-470">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="afa81-470">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="afa81-471">To create a two-tier system by using only one virtual machine, use this template.</span><span class="sxs-lookup"><span data-stu-id="afa81-471">To create a two-tier system by using only one virtual machine, use this template.</span></span>

<span data-ttu-id="afa81-472">In the Azure portal, enter the following parameters for the template:</span><span class="sxs-lookup"><span data-stu-id="afa81-472">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="afa81-473">**Basics**:</span><span class="sxs-lookup"><span data-stu-id="afa81-473">**Basics**:</span></span>
  * <span data-ttu-id="afa81-474">**Subscription**: The subscription to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-474">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="afa81-475">**Resource group**: The resource group to use to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-475">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="afa81-476">You can create a new resource group or select an existing resource group in the subscription.</span><span class="sxs-lookup"><span data-stu-id="afa81-476">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="afa81-477">**Location**: Where to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="afa81-477">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="afa81-478">If you selected an existing resource group, the location of that resource group is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-478">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="afa81-479">**Settings**:</span><span class="sxs-lookup"><span data-stu-id="afa81-479">**Settings**:</span></span>
  * <span data-ttu-id="afa81-480">**SAP System ID**: The SAP System ID.</span><span class="sxs-lookup"><span data-stu-id="afa81-480">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="afa81-481">**OS type**: The operating system type you want to deploy (Windows or Linux).</span><span class="sxs-lookup"><span data-stu-id="afa81-481">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="afa81-482">**SAP system size**: The size of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="afa81-482">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="afa81-483">The number of SAPS the new system provides.</span><span class="sxs-lookup"><span data-stu-id="afa81-483">The number of SAPS the new system provides.</span></span> <span data-ttu-id="afa81-484">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="afa81-484">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="afa81-485">**Storage type** (two-tier template only): The type of storage to use.</span><span class="sxs-lookup"><span data-stu-id="afa81-485">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="afa81-486">For larger systems, we highly recommend using Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="afa81-486">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="afa81-487">For more information about storage types, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="afa81-487">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="afa81-488">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span><span class="sxs-lookup"><span data-stu-id="afa81-488">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="afa81-489">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP on Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="afa81-489">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="afa81-490">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="afa81-490">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="afa81-491">[Introduction to Microsoft Azure Storage][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="afa81-491">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="afa81-492">**OS disk VHD URI**: The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span><span class="sxs-lookup"><span data-stu-id="afa81-492">**OS disk VHD URI**: The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="afa81-493">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span><span class="sxs-lookup"><span data-stu-id="afa81-493">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="afa81-494">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span><span class="sxs-lookup"><span data-stu-id="afa81-494">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="afa81-495">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span><span class="sxs-lookup"><span data-stu-id="afa81-495">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="afa81-496">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="afa81-496">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="afa81-497">The ID usually looks like this:</span><span class="sxs-lookup"><span data-stu-id="afa81-497">The ID usually looks like this:</span></span>

    <span data-ttu-id="afa81-498">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span><span class="sxs-lookup"><span data-stu-id="afa81-498">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="afa81-499">**Terms and conditions**:</span><span class="sxs-lookup"><span data-stu-id="afa81-499">**Terms and conditions**:</span></span>  
    <span data-ttu-id="afa81-500">Review and accept the legal terms.</span><span class="sxs-lookup"><span data-stu-id="afa81-500">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="afa81-501">Select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="afa81-501">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent"></a><span data-ttu-id="afa81-502">Install the VM Agent</span><span class="sxs-lookup"><span data-stu-id="afa81-502">Install the VM Agent</span></span>
<span data-ttu-id="afa81-503">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="afa81-503">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span></span> <span data-ttu-id="afa81-504">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span><span class="sxs-lookup"><span data-stu-id="afa81-504">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="afa81-505">If you don’t use the templates described in the preceding section, you can also install the VM Agent afterwards.</span><span class="sxs-lookup"><span data-stu-id="afa81-505">If you don’t use the templates described in the preceding section, you can also install the VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="afa81-506">Join a domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="afa81-506">Join a domain (Windows only)</span></span>
<span data-ttu-id="afa81-507">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="afa81-507">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="afa81-508">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-508">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="afa81-509">Configure proxy settings</span><span class="sxs-lookup"><span data-stu-id="afa81-509">Configure proxy settings</span></span>
<span data-ttu-id="afa81-510">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-510">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="afa81-511">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span><span class="sxs-lookup"><span data-stu-id="afa81-511">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="afa81-512">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="afa81-512">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="afa81-513">Configure monitoring</span><span class="sxs-lookup"><span data-stu-id="afa81-513">Configure monitoring</span></span>
<span data-ttu-id="afa81-514">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-514">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="afa81-515">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-515">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="afa81-516">Monitoring check</span><span class="sxs-lookup"><span data-stu-id="afa81-516">Monitoring check</span></span>
<span data-ttu-id="afa81-517">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span><span class="sxs-lookup"><span data-stu-id="afa81-517">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-the-monitoring-configuration-for-sap"></a><span data-ttu-id="afa81-518">Update the monitoring configuration for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-518">Update the monitoring configuration for SAP</span></span>
<span data-ttu-id="afa81-519">Update the SAP monitoring configuration in any of the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="afa81-519">Update the SAP monitoring configuration in any of the following scenarios:</span></span>
* <span data-ttu-id="afa81-520">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span><span class="sxs-lookup"><span data-stu-id="afa81-520">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="afa81-521">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span><span class="sxs-lookup"><span data-stu-id="afa81-521">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span></span>
* <span data-ttu-id="afa81-522">You mount additional VHDs to your Azure VM or you remove a VHD.</span><span class="sxs-lookup"><span data-stu-id="afa81-522">You mount additional VHDs to your Azure VM or you remove a VHD.</span></span> <span data-ttu-id="afa81-523">In this scenario, update the collection of storage-related data.</span><span class="sxs-lookup"><span data-stu-id="afa81-523">In this scenario, update the collection of storage-related data.</span></span> <span data-ttu-id="afa81-524">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="afa81-524">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span></span>
* <span data-ttu-id="afa81-525">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span><span class="sxs-lookup"><span data-stu-id="afa81-525">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span></span>
* <span data-ttu-id="afa81-526">You add new network interfaces to your Azure VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-526">You add new network interfaces to your Azure VM.</span></span>

<span data-ttu-id="afa81-527">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-527">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment-on-a-linux-vm"></a><span data-ttu-id="afa81-528">Detailed tasks for SAP software deployment on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="afa81-528">Detailed tasks for SAP software deployment on a Linux VM</span></span>
<span data-ttu-id="afa81-529">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span><span class="sxs-lookup"><span data-stu-id="afa81-529">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span></span>

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a><span data-ttu-id="afa81-530">Deploy Azure PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="afa81-530">Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="afa81-531">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="afa81-531">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="afa81-532">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span><span class="sxs-lookup"><span data-stu-id="afa81-532">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="afa81-533">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span><span class="sxs-lookup"><span data-stu-id="afa81-533">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="afa81-534">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="afa81-534">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="afa81-535">A page that looks like this appears:</span><span class="sxs-lookup"><span data-stu-id="afa81-535">A page that looks like this appears:</span></span>

  <span data-ttu-id="afa81-536">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-536">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="afa81-537">Select **Install**, and then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="afa81-537">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="afa81-538">PowerShell is installed.</span><span class="sxs-lookup"><span data-stu-id="afa81-538">PowerShell is installed.</span></span> <span data-ttu-id="afa81-539">Select **Finish** to close the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="afa81-539">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="afa81-540">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span><span class="sxs-lookup"><span data-stu-id="afa81-540">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="afa81-541">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="afa81-541">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span> <span data-ttu-id="afa81-542">The release date and release number of the cmdlets are included on the page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="afa81-542">The release date and release number of the cmdlets are included on the page shown in step 5.</span></span> <span data-ttu-id="afa81-543">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="afa81-543">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="afa81-544">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="afa81-544">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
<span data-ttu-id="afa81-545">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="afa81-545">The result looks like this:</span></span>

<span data-ttu-id="afa81-546">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-546">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="afa81-547">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span><span class="sxs-lookup"><span data-stu-id="afa81-547">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span></span> <span data-ttu-id="afa81-548">Your PowerShell Azure cmdlets are up-to-date.</span><span class="sxs-lookup"><span data-stu-id="afa81-548">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="afa81-549">To close the installation wizard, select **Exit**.</span><span class="sxs-lookup"><span data-stu-id="afa81-549">To close the installation wizard, select **Exit**.</span></span>

<span data-ttu-id="afa81-550">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-550">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a><span data-ttu-id="afa81-551">Deploy Azure CLI</span><span class="sxs-lookup"><span data-stu-id="afa81-551">Deploy Azure CLI</span></span>
1.  <span data-ttu-id="afa81-552">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="afa81-552">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="afa81-553">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span><span class="sxs-lookup"><span data-stu-id="afa81-553">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="afa81-554">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span><span class="sxs-lookup"><span data-stu-id="afa81-554">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="afa81-555">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="afa81-555">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="afa81-556">A page that looks like this appears:</span><span class="sxs-lookup"><span data-stu-id="afa81-556">A page that looks like this appears:</span></span>

  <span data-ttu-id="afa81-557">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-557">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="afa81-558">Select **Install**, and then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="afa81-558">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="afa81-559">Azure CLI is installed.</span><span class="sxs-lookup"><span data-stu-id="afa81-559">Azure CLI is installed.</span></span> <span data-ttu-id="afa81-560">Select **Finish** to close the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="afa81-560">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="afa81-561">Check frequently for updates to Azure CLI, which usually is updated monthly.</span><span class="sxs-lookup"><span data-stu-id="afa81-561">Check frequently for updates to Azure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="afa81-562">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span><span class="sxs-lookup"><span data-stu-id="afa81-562">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span>

<span data-ttu-id="afa81-563">To check the version of Azure CLI that is installed on your computer, run this command:</span><span class="sxs-lookup"><span data-stu-id="afa81-563">To check the version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="afa81-564">The result looks like this:</span><span class="sxs-lookup"><span data-stu-id="afa81-564">The result looks like this:</span></span>

<span data-ttu-id="afa81-565">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-565">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a><span data-ttu-id="afa81-566">Join a VM to an on-premises domain (Windows only)</span><span class="sxs-lookup"><span data-stu-id="afa81-566">Join a VM to an on-premises domain (Windows only)</span></span>
<span data-ttu-id="afa81-567">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="afa81-567">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span></span> <span data-ttu-id="afa81-568">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span><span class="sxs-lookup"><span data-stu-id="afa81-568">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="afa81-569">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span><span class="sxs-lookup"><span data-stu-id="afa81-569">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="afa81-570">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span><span class="sxs-lookup"><span data-stu-id="afa81-570">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span></span> <span data-ttu-id="afa81-571">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span><span class="sxs-lookup"><span data-stu-id="afa81-571">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span></span>

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a><span data-ttu-id="afa81-572">Download, install, and enable the Azure VM Agent</span><span class="sxs-lookup"><span data-stu-id="afa81-572">Download, install, and enable the Azure VM Agent</span></span>
<span data-ttu-id="afa81-573">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="afa81-573">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span></span>

<span data-ttu-id="afa81-574">If you deploy a VM from the Azure Marketplace, this step is not required.</span><span class="sxs-lookup"><span data-stu-id="afa81-574">If you deploy a VM from the Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="afa81-575">Images from the Azure Marketplace already have the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="afa81-575">Images from the Azure Marketplace already have the Azure VM Agent.</span></span>

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a><span data-ttu-id="afa81-576">Windows</span><span class="sxs-lookup"><span data-stu-id="afa81-576">Windows</span></span>
1.  <span data-ttu-id="afa81-577">Download the Azure VM Agent:</span><span class="sxs-lookup"><span data-stu-id="afa81-577">Download the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="afa81-578">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span><span class="sxs-lookup"><span data-stu-id="afa81-578">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="afa81-579">Store the VM Agent MSI package locally on a personal computer or server.</span><span class="sxs-lookup"><span data-stu-id="afa81-579">Store the VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="afa81-580">Install the Azure VM Agent:</span><span class="sxs-lookup"><span data-stu-id="afa81-580">Install the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="afa81-581">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="afa81-581">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="afa81-582">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="afa81-582">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span></span>
  3.  <span data-ttu-id="afa81-583">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-583">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span></span>
  4.  <span data-ttu-id="afa81-584">Double-click the MSI file on the VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-584">Double-click the MSI file on the VM.</span></span>
3.  <span data-ttu-id="afa81-585">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="afa81-585">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="afa81-586">The VM Agent runs in this context and needs to be able to connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-586">The VM Agent runs in this context and needs to be able to connect to Azure.</span></span>

<span data-ttu-id="afa81-587">No user interaction is required to update the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="afa81-587">No user interaction is required to update the Azure VM Agent.</span></span> <span data-ttu-id="afa81-588">The VM Agent is automatically updated, and does not require a VM restart.</span><span class="sxs-lookup"><span data-stu-id="afa81-588">The VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a><span data-ttu-id="afa81-589">Linux</span><span class="sxs-lookup"><span data-stu-id="afa81-589">Linux</span></span>
<span data-ttu-id="afa81-590">Use the following commands to install the VM Agent for Linux:</span><span class="sxs-lookup"><span data-stu-id="afa81-590">Use the following commands to install the VM Agent for Linux:</span></span>

* <span data-ttu-id="afa81-591">**SUSE Linux Enterprise Server (SLES)**</span><span class="sxs-lookup"><span data-stu-id="afa81-591">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="afa81-592">**Red Hat Enterprise Linux (RHEL)**</span><span class="sxs-lookup"><span data-stu-id="afa81-592">**Red Hat Enterprise Linux (RHEL)**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="afa81-593">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span><span class="sxs-lookup"><span data-stu-id="afa81-593">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a><span data-ttu-id="afa81-594">Configure the proxy</span><span class="sxs-lookup"><span data-stu-id="afa81-594">Configure the proxy</span></span>
<span data-ttu-id="afa81-595">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span><span class="sxs-lookup"><span data-stu-id="afa81-595">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="afa81-596">Windows</span><span class="sxs-lookup"><span data-stu-id="afa81-596">Windows</span></span>
<span data-ttu-id="afa81-597">Proxy settings must be set up correctly for the Local System account to access the Internet.</span><span class="sxs-lookup"><span data-stu-id="afa81-597">Proxy settings must be set up correctly for the Local System account to access the Internet.</span></span> <span data-ttu-id="afa81-598">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span><span class="sxs-lookup"><span data-stu-id="afa81-598">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span></span>

1. <span data-ttu-id="afa81-599">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="afa81-599">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="afa81-600">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="afa81-600">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="afa81-601">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span><span class="sxs-lookup"><span data-stu-id="afa81-601">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="afa81-602">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span><span class="sxs-lookup"><span data-stu-id="afa81-602">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="afa81-603">On the **Connections** tab, select the **LAN settings** button.</span><span class="sxs-lookup"><span data-stu-id="afa81-603">On the **Connections** tab, select the **LAN settings** button.</span></span>
5. <span data-ttu-id="afa81-604">Clear the **Automatically detect settings** check box.</span><span class="sxs-lookup"><span data-stu-id="afa81-604">Clear the **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="afa81-605">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span><span class="sxs-lookup"><span data-stu-id="afa81-605">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span></span>
7. <span data-ttu-id="afa81-606">Select the **Advanced** button.</span><span class="sxs-lookup"><span data-stu-id="afa81-606">Select the **Advanced** button.</span></span>
8. <span data-ttu-id="afa81-607">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span><span class="sxs-lookup"><span data-stu-id="afa81-607">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span></span> <span data-ttu-id="afa81-608">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="afa81-608">Select **OK**.</span></span>

#### <a name="linux"></a><span data-ttu-id="afa81-609">Linux</span><span class="sxs-lookup"><span data-stu-id="afa81-609">Linux</span></span>
<span data-ttu-id="afa81-610">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span><span class="sxs-lookup"><span data-stu-id="afa81-610">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="afa81-611">Set the following parameters:</span><span class="sxs-lookup"><span data-stu-id="afa81-611">Set the following parameters:</span></span>

1.  <span data-ttu-id="afa81-612">**HTTP proxy host**.</span><span class="sxs-lookup"><span data-stu-id="afa81-612">**HTTP proxy host**.</span></span> <span data-ttu-id="afa81-613">For example, set it to **proxy.corp.local**.</span><span class="sxs-lookup"><span data-stu-id="afa81-613">For example, set it to **proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="afa81-614">**HTTP proxy port**.</span><span class="sxs-lookup"><span data-stu-id="afa81-614">**HTTP proxy port**.</span></span> <span data-ttu-id="afa81-615">For example, set it to **80**.</span><span class="sxs-lookup"><span data-stu-id="afa81-615">For example, set it to **80**.</span></span>
  ```
  HttpProxy.Port=<port of the proxy host>

  ```
3.  <span data-ttu-id="afa81-616">Restart the agent.</span><span class="sxs-lookup"><span data-stu-id="afa81-616">Restart the agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="afa81-617">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span><span class="sxs-lookup"><span data-stu-id="afa81-617">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span></span> <span data-ttu-id="afa81-618">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span><span class="sxs-lookup"><span data-stu-id="afa81-618">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="afa81-619">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span><span class="sxs-lookup"><span data-stu-id="afa81-619">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="afa81-620">**SLES**</span><span class="sxs-lookup"><span data-stu-id="afa81-620">**SLES**</span></span>

  <span data-ttu-id="afa81-621">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span><span class="sxs-lookup"><span data-stu-id="afa81-621">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="afa81-622">The following figure shows an example:</span><span class="sxs-lookup"><span data-stu-id="afa81-622">The following figure shows an example:</span></span>

  ![Forced tunneling][deployment-guide-figure-50]


* <span data-ttu-id="afa81-624">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="afa81-624">**RHEL**</span></span>

  <span data-ttu-id="afa81-625">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span><span class="sxs-lookup"><span data-stu-id="afa81-625">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="afa81-626">For an example, see the preceding figure.</span><span class="sxs-lookup"><span data-stu-id="afa81-626">For an example, see the preceding figure.</span></span>

<span data-ttu-id="afa81-627">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span><span class="sxs-lookup"><span data-stu-id="afa81-627">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a><span data-ttu-id="afa81-628">Configure the Azure Enhanced Monitoring Extension for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-628">Configure the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="afa81-629">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-629">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="afa81-630">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="afa81-630">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span></span> <span data-ttu-id="afa81-631">For more information, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide-9.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-631">For more information, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide-9.1].</span></span>

<span data-ttu-id="afa81-632">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span><span class="sxs-lookup"><span data-stu-id="afa81-632">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="afa81-633">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-633">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="afa81-634">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-634">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a><span data-ttu-id="afa81-635">Azure PowerShell for Linux and Windows VMs</span><span class="sxs-lookup"><span data-stu-id="afa81-635">Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="afa81-636">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="afa81-636">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="afa81-637">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afa81-637">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span></span> <span data-ttu-id="afa81-638">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-638">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="afa81-639">Run the following PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afa81-639">Run the following PowerShell cmdlet.</span></span>
    <span data-ttu-id="afa81-640">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="afa81-640">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="afa81-641">If you want to use public Azure, your environment is **AzureCloud**.</span><span class="sxs-lookup"><span data-stu-id="afa81-641">If you want to use public Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="afa81-642">For Azure in China, select **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="afa81-642">For Azure in China, select **AzureChinaCloud**.</span></span>

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of the environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

<span data-ttu-id="afa81-643">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span><span class="sxs-lookup"><span data-stu-id="afa81-643">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span></span> <span data-ttu-id="afa81-644">This can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="afa81-644">This can take several minutes.</span></span>
<span data-ttu-id="afa81-645">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span><span class="sxs-lookup"><span data-stu-id="afa81-645">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![Successful execution of SAP-specific Azure cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

<span data-ttu-id="afa81-647">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span><span class="sxs-lookup"><span data-stu-id="afa81-647">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span></span>

<span data-ttu-id="afa81-648">The script output includes the following information:</span><span class="sxs-lookup"><span data-stu-id="afa81-648">The script output includes the following information:</span></span>

* <span data-ttu-id="afa81-649">Confirmation that monitoring for the base VHD (with the OS) and all additional VHDs mounted to the VM has been configured.</span><span class="sxs-lookup"><span data-stu-id="afa81-649">Confirmation that monitoring for the base VHD (with the OS) and all additional VHDs mounted to the VM has been configured.</span></span>
* <span data-ttu-id="afa81-650">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span><span class="sxs-lookup"><span data-stu-id="afa81-650">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="afa81-651">One line of output gives the status of the actual update of the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="afa81-651">One line of output gives the status of the actual update of the monitoring configuration.</span></span>
* <span data-ttu-id="afa81-652">Another line of output confirms that the configuration has been deployed or updated.</span><span class="sxs-lookup"><span data-stu-id="afa81-652">Another line of output confirms that the configuration has been deployed or updated.</span></span>
* <span data-ttu-id="afa81-653">The last line of output is informational.</span><span class="sxs-lookup"><span data-stu-id="afa81-653">The last line of output is informational.</span></span> <span data-ttu-id="afa81-654">It shows your options for testing the monitoring configuration.</span><span class="sxs-lookup"><span data-stu-id="afa81-654">It shows your options for testing the monitoring configuration.</span></span>
* <span data-ttu-id="afa81-655">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-655">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span>
* <span data-ttu-id="afa81-656">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span><span class="sxs-lookup"><span data-stu-id="afa81-656">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span></span>

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a><span data-ttu-id="afa81-657">Azure CLI for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="afa81-657">Azure CLI for Linux VMs</span></span>
<span data-ttu-id="afa81-658">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="afa81-658">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="afa81-659">Install Azure CLI, as described in [Install the Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="afa81-659">Install Azure CLI, as described in [Install the Azure CLI][azure-cli].</span></span>
2. <span data-ttu-id="afa81-660">Sign in with your Azure account:</span><span class="sxs-lookup"><span data-stu-id="afa81-660">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="afa81-661">Switch to Azure Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="afa81-661">Switch to Azure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="afa81-662">Enable Azure Enhanced Monitoring:</span><span class="sxs-lookup"><span data-stu-id="afa81-662">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="afa81-663">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-663">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span></span> <span data-ttu-id="afa81-664">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span><span class="sxs-lookup"><span data-stu-id="afa81-664">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="afa81-665">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span><span class="sxs-lookup"><span data-stu-id="afa81-665">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="afa81-666">The output looks like this:</span><span class="sxs-lookup"><span data-stu-id="afa81-666">The output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a><span data-ttu-id="afa81-667">Checks and troubleshooting for end-to-end monitoring</span><span class="sxs-lookup"><span data-stu-id="afa81-667">Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="afa81-668">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span><span class="sxs-lookup"><span data-stu-id="afa81-668">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="afa81-669">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-669">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="afa81-670">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring successfully set up.</span><span class="sxs-lookup"><span data-stu-id="afa81-670">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring successfully set up.</span></span> <span data-ttu-id="afa81-671">You can proceed with the installation of SAP Host Agent described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-671">You can proceed with the installation of SAP Host Agent described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="afa81-672">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-672">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="afa81-673">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-673">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a><span data-ttu-id="afa81-674">Readiness check for the Azure Enhanced Monitoring Extension for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-674">Readiness check for the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="afa81-675">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span><span class="sxs-lookup"><span data-stu-id="afa81-675">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-the-readiness-check-on-a-windows-vm"></a><span data-ttu-id="afa81-676">Run the readiness check on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="afa81-676">Run the readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="afa81-677">Sign in to the Azure virtual machine (using an admin account is not necessary).</span><span class="sxs-lookup"><span data-stu-id="afa81-677">Sign in to the Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="afa81-678">Open a Command Prompt window.</span><span class="sxs-lookup"><span data-stu-id="afa81-678">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="afa81-679">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span><span class="sxs-lookup"><span data-stu-id="afa81-679">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="afa81-680">The *version* in the path to the monitoring extension might vary.</span><span class="sxs-lookup"><span data-stu-id="afa81-680">The *version* in the path to the monitoring extension might vary.</span></span> <span data-ttu-id="afa81-681">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span><span class="sxs-lookup"><span data-stu-id="afa81-681">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span></span>

  ![Properties of service running the Azure Enhanced Monitoring Extension for SAP][deployment-guide-figure-1000]

4.  <span data-ttu-id="afa81-683">At the command prompt, run **azperflib.exe** without any parameters.</span><span class="sxs-lookup"><span data-stu-id="afa81-683">At the command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="afa81-684">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="afa81-684">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span></span> <span data-ttu-id="afa81-685">To end the loop, close the Command Prompt window.</span><span class="sxs-lookup"><span data-stu-id="afa81-685">To end the loop, close the Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="afa81-686">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span><span class="sxs-lookup"><span data-stu-id="afa81-686">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span></span> <span data-ttu-id="afa81-687">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-687">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-the-output-of-azperflibexe"></a><span data-ttu-id="afa81-688">Check the output of azperflib.exe</span><span class="sxs-lookup"><span data-stu-id="afa81-688">Check the output of azperflib.exe</span></span>
<span data-ttu-id="afa81-689">Azperflib.exe output shows all populated Azure performance counters for SAP.</span><span class="sxs-lookup"><span data-stu-id="afa81-689">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="afa81-690">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span><span class="sxs-lookup"><span data-stu-id="afa81-690">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span></span>

<span data-ttu-id="afa81-691">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-691">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="afa81-692">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span><span class="sxs-lookup"><span data-stu-id="afa81-692">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span></span>

<span data-ttu-id="afa81-693">Interpret the resulting values as follows:</span><span class="sxs-lookup"><span data-stu-id="afa81-693">Interpret the resulting values as follows:</span></span>

| <span data-ttu-id="afa81-694">Azperflib.exe result values</span><span class="sxs-lookup"><span data-stu-id="afa81-694">Azperflib.exe result values</span></span> | <span data-ttu-id="afa81-695">Azure monitoring health status</span><span class="sxs-lookup"><span data-stu-id="afa81-695">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="afa81-696">**API Calls - not available**</span><span class="sxs-lookup"><span data-stu-id="afa81-696">**API Calls - not available**</span></span> | <span data-ttu-id="afa81-697">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span><span class="sxs-lookup"><span data-stu-id="afa81-697">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span></span> <span data-ttu-id="afa81-698">See **Health status**.</span><span class="sxs-lookup"><span data-stu-id="afa81-698">See **Health status**.</span></span> |
| <span data-ttu-id="afa81-699">**Counters total - empty**</span><span class="sxs-lookup"><span data-stu-id="afa81-699">**Counters total - empty**</span></span> |<span data-ttu-id="afa81-700">The following two Azure storage counters can be empty:</span><span class="sxs-lookup"><span data-stu-id="afa81-700">The following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="afa81-701">Storage Read Op Latency Server msec</span><span class="sxs-lookup"><span data-stu-id="afa81-701">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="afa81-702">Storage Read Op Latency E2E msec</span><span class="sxs-lookup"><span data-stu-id="afa81-702">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="afa81-703">All other counters must have values.</span><span class="sxs-lookup"><span data-stu-id="afa81-703">All other counters must have values.</span></span> |
| <span data-ttu-id="afa81-704">**Health status**</span><span class="sxs-lookup"><span data-stu-id="afa81-704">**Health status**</span></span> |<span data-ttu-id="afa81-705">Only OK if return status shows **OK**.</span><span class="sxs-lookup"><span data-stu-id="afa81-705">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="afa81-706">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="afa81-706">**Diagnostics**</span></span> |<span data-ttu-id="afa81-707">Detailed information about health status.</span><span class="sxs-lookup"><span data-stu-id="afa81-707">Detailed information about health status.</span></span> |

<span data-ttu-id="afa81-708">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-708">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-the-readiness-check-on-a-linux-vm"></a><span data-ttu-id="afa81-709">Run the readiness check on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="afa81-709">Run the readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="afa81-710">Connect to the Azure Virtual Machine by using SSH.</span><span class="sxs-lookup"><span data-stu-id="afa81-710">Connect to the Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="afa81-711">Check the output of the Azure Enhanced Monitoring Extension.</span><span class="sxs-lookup"><span data-stu-id="afa81-711">Check the output of the Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="afa81-712">a.</span><span class="sxs-lookup"><span data-stu-id="afa81-712">a.</span></span>  <span data-ttu-id="afa81-713">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span><span class="sxs-lookup"><span data-stu-id="afa81-713">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="afa81-714">**Expected result**: Returns list of performance counters.</span><span class="sxs-lookup"><span data-stu-id="afa81-714">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="afa81-715">The file should not be empty.</span><span class="sxs-lookup"><span data-stu-id="afa81-715">The file should not be empty.</span></span>

 <span data-ttu-id="afa81-716">b.</span><span class="sxs-lookup"><span data-stu-id="afa81-716">b.</span></span> <span data-ttu-id="afa81-717">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span><span class="sxs-lookup"><span data-stu-id="afa81-717">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="afa81-718">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span><span class="sxs-lookup"><span data-stu-id="afa81-718">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="afa81-719">c.</span><span class="sxs-lookup"><span data-stu-id="afa81-719">c.</span></span> <span data-ttu-id="afa81-720">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span><span class="sxs-lookup"><span data-stu-id="afa81-720">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="afa81-721">**Expected result**: Returns as empty or does not exist.</span><span class="sxs-lookup"><span data-stu-id="afa81-721">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="afa81-722">If the preceding check was not successful, run these additional checks:</span><span class="sxs-lookup"><span data-stu-id="afa81-722">If the preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="afa81-723">Make sure that the waagent is installed and enabled.</span><span class="sxs-lookup"><span data-stu-id="afa81-723">Make sure that the waagent is installed and enabled.</span></span>

  <span data-ttu-id="afa81-724">a.</span><span class="sxs-lookup"><span data-stu-id="afa81-724">a.</span></span>  <span data-ttu-id="afa81-725">Run `sudo ls -al /var/lib/waagent/`</span><span class="sxs-lookup"><span data-stu-id="afa81-725">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="afa81-726">**Expected result**: Lists the content of the waagent directory.</span><span class="sxs-lookup"><span data-stu-id="afa81-726">**Expected result**: Lists the content of the waagent directory.</span></span>

  <span data-ttu-id="afa81-727">b.</span><span class="sxs-lookup"><span data-stu-id="afa81-727">b.</span></span>  <span data-ttu-id="afa81-728">Run `ps -ax | grep waagent`</span><span class="sxs-lookup"><span data-stu-id="afa81-728">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="afa81-729">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="afa81-729">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

2. <span data-ttu-id="afa81-730">Make sure that the Linux Diagnostic Extension is installed and enabled.</span><span class="sxs-lookup"><span data-stu-id="afa81-730">Make sure that the Linux Diagnostic Extension is installed and enabled.</span></span>

  <span data-ttu-id="afa81-731">a.</span><span class="sxs-lookup"><span data-stu-id="afa81-731">a.</span></span>  <span data-ttu-id="afa81-732">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`</span><span class="sxs-lookup"><span data-stu-id="afa81-732">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`</span></span>

   <span data-ttu-id="afa81-733">**Expected result**: Lists the content of the Linux Diagnostic Extension directory.</span><span class="sxs-lookup"><span data-stu-id="afa81-733">**Expected result**: Lists the content of the Linux Diagnostic Extension directory.</span></span>

 <span data-ttu-id="afa81-734">b.</span><span class="sxs-lookup"><span data-stu-id="afa81-734">b.</span></span> <span data-ttu-id="afa81-735">Run `ps -ax | grep diagnostic`</span><span class="sxs-lookup"><span data-stu-id="afa81-735">Run `ps -ax | grep diagnostic`</span></span>

   <span data-ttu-id="afa81-736">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span><span class="sxs-lookup"><span data-stu-id="afa81-736">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span></span>

3.   <span data-ttu-id="afa81-737">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span><span class="sxs-lookup"><span data-stu-id="afa81-737">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="afa81-738">a.</span><span class="sxs-lookup"><span data-stu-id="afa81-738">a.</span></span>  <span data-ttu-id="afa81-739">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`</span><span class="sxs-lookup"><span data-stu-id="afa81-739">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`</span></span>

    <span data-ttu-id="afa81-740">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span><span class="sxs-lookup"><span data-stu-id="afa81-740">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="afa81-741">b.</span><span class="sxs-lookup"><span data-stu-id="afa81-741">b.</span></span> <span data-ttu-id="afa81-742">Run `ps -ax | grep AzureEnhanced`</span><span class="sxs-lookup"><span data-stu-id="afa81-742">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="afa81-743">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="afa81-743">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="afa81-744">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span><span class="sxs-lookup"><span data-stu-id="afa81-744">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span></span>

  <span data-ttu-id="afa81-745">a.</span><span class="sxs-lookup"><span data-stu-id="afa81-745">a.</span></span>  <span data-ttu-id="afa81-746">Run `/usr/sap/hostctrl/exe/saposcol -d`</span><span class="sxs-lookup"><span data-stu-id="afa81-746">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="afa81-747">b.</span><span class="sxs-lookup"><span data-stu-id="afa81-747">b.</span></span>  <span data-ttu-id="afa81-748">Run `dump ccm`</span><span class="sxs-lookup"><span data-stu-id="afa81-748">Run `dump ccm`</span></span>

  <span data-ttu-id="afa81-749">c.</span><span class="sxs-lookup"><span data-stu-id="afa81-749">c.</span></span>  <span data-ttu-id="afa81-750">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span><span class="sxs-lookup"><span data-stu-id="afa81-750">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="afa81-751">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span><span class="sxs-lookup"><span data-stu-id="afa81-751">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="afa81-752">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-752">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a><span data-ttu-id="afa81-753">Health check for the Azure monitoring infrastructure configuration</span><span class="sxs-lookup"><span data-stu-id="afa81-753">Health check for the Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="afa81-754">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span><span class="sxs-lookup"><span data-stu-id="afa81-754">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="afa81-755">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span><span class="sxs-lookup"><span data-stu-id="afa81-755">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="afa81-756">Run the following PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afa81-756">Run the following PowerShell cmdlet.</span></span> <span data-ttu-id="afa81-757">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="afa81-757">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="afa81-758">To use public Azure, select the **AzureCloud** environment.</span><span class="sxs-lookup"><span data-stu-id="afa81-758">To use public Azure, select the **AzureCloud** environment.</span></span> <span data-ttu-id="afa81-759">For Azure in China, select **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="afa81-759">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of the environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="afa81-760">Enter your account data and identify the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-760">Enter your account data and identify the Azure virtual machine.</span></span>

  ![Input page of SAP-specific Azure cmdlet Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. <span data-ttu-id="afa81-762">The script tests the configuration of the virtual machine you select.</span><span class="sxs-lookup"><span data-stu-id="afa81-762">The script tests the configuration of the virtual machine you select.</span></span>

  ![Output of successful test of the Azure monitoring infrastructure for SAP][deployment-guide-figure-1300]

<span data-ttu-id="afa81-764">Make sure that every health check result is **OK**.</span><span class="sxs-lookup"><span data-stu-id="afa81-764">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="afa81-765">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-765">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="afa81-766">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="afa81-766">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="afa81-767">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span><span class="sxs-lookup"><span data-stu-id="afa81-767">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a><span data-ttu-id="afa81-768">Troubleshooting the Azure monitoring infrastructure for SAP</span><span class="sxs-lookup"><span data-stu-id="afa81-768">Troubleshooting the Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="afa81-770">Azure performance counters do not show up at all</span><span class="sxs-lookup"><span data-stu-id="afa81-770">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="afa81-771">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-771">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="afa81-772">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span><span class="sxs-lookup"><span data-stu-id="afa81-772">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="afa81-773">The installation directory of the Azure Enhanced Monitoring Extension is empty</span><span class="sxs-lookup"><span data-stu-id="afa81-773">The installation directory of the Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="afa81-774">Issue</span><span class="sxs-lookup"><span data-stu-id="afa81-774">Issue</span></span>
<span data-ttu-id="afa81-775">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span><span class="sxs-lookup"><span data-stu-id="afa81-775">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="afa81-776">Solution</span><span class="sxs-lookup"><span data-stu-id="afa81-776">Solution</span></span>
<span data-ttu-id="afa81-777">The extension is not installed.</span><span class="sxs-lookup"><span data-stu-id="afa81-777">The extension is not installed.</span></span> <span data-ttu-id="afa81-778">Determine whether this is a proxy issue (as described earlier).</span><span class="sxs-lookup"><span data-stu-id="afa81-778">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="afa81-779">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="afa81-779">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="afa81-780">Service for Azure Enhanced Monitoring does not exist</span><span class="sxs-lookup"><span data-stu-id="afa81-780">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="afa81-781">Issue</span><span class="sxs-lookup"><span data-stu-id="afa81-781">Issue</span></span>
<span data-ttu-id="afa81-782">The AzureEnhancedMonitoring Windows service does not exist.</span><span class="sxs-lookup"><span data-stu-id="afa81-782">The AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="afa81-783">Azperflib.exe output throws an error:</span><span class="sxs-lookup"><span data-stu-id="afa81-783">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="afa81-784">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="afa81-784">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="afa81-785">Solution</span><span class="sxs-lookup"><span data-stu-id="afa81-785">Solution</span></span>
<span data-ttu-id="afa81-786">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span><span class="sxs-lookup"><span data-stu-id="afa81-786">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="afa81-787">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span><span class="sxs-lookup"><span data-stu-id="afa81-787">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="afa81-788">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="afa81-788">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-to-start"></a><span data-ttu-id="afa81-789">Service for Azure Enhanced Monitoring exists, but fails to start</span><span class="sxs-lookup"><span data-stu-id="afa81-789">Service for Azure Enhanced Monitoring exists, but fails to start</span></span>

###### <a name="issue"></a><span data-ttu-id="afa81-790">Issue</span><span class="sxs-lookup"><span data-stu-id="afa81-790">Issue</span></span>
<span data-ttu-id="afa81-791">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span><span class="sxs-lookup"><span data-stu-id="afa81-791">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span></span> <span data-ttu-id="afa81-792">For more information, check the application event log.</span><span class="sxs-lookup"><span data-stu-id="afa81-792">For more information, check the application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="afa81-793">Solution</span><span class="sxs-lookup"><span data-stu-id="afa81-793">Solution</span></span>
<span data-ttu-id="afa81-794">The configuration is incorrect.</span><span class="sxs-lookup"><span data-stu-id="afa81-794">The configuration is incorrect.</span></span> <span data-ttu-id="afa81-795">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-795">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="afa81-797">Some Azure performance counters are missing</span><span class="sxs-lookup"><span data-stu-id="afa81-797">Some Azure performance counters are missing</span></span>
<span data-ttu-id="afa81-798">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span><span class="sxs-lookup"><span data-stu-id="afa81-798">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="afa81-799">The service gets data from several sources.</span><span class="sxs-lookup"><span data-stu-id="afa81-799">The service gets data from several sources.</span></span> <span data-ttu-id="afa81-800">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="afa81-800">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="afa81-801">Storage counters are used from your logging on the storage subscription level.</span><span class="sxs-lookup"><span data-stu-id="afa81-801">Storage counters are used from your logging on the storage subscription level.</span></span>

<span data-ttu-id="afa81-802">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="afa81-802">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="afa81-803">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span><span class="sxs-lookup"><span data-stu-id="afa81-803">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="afa81-804">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-804">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="afa81-806">Azure performance counters do not show up at all</span><span class="sxs-lookup"><span data-stu-id="afa81-806">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="afa81-807">Performance metrics in Azure are collected by a daemon.</span><span class="sxs-lookup"><span data-stu-id="afa81-807">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="afa81-808">If the daemon is not running, no performance metrics can be collected.</span><span class="sxs-lookup"><span data-stu-id="afa81-808">If the daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="afa81-809">The installation directory of the Azure Enhanced Monitoring extension is empty</span><span class="sxs-lookup"><span data-stu-id="afa81-809">The installation directory of the Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="afa81-810">Issue</span><span class="sxs-lookup"><span data-stu-id="afa81-810">Issue</span></span>
<span data-ttu-id="afa81-811">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span><span class="sxs-lookup"><span data-stu-id="afa81-811">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="afa81-812">Solution</span><span class="sxs-lookup"><span data-stu-id="afa81-812">Solution</span></span>
<span data-ttu-id="afa81-813">The extension is not installed.</span><span class="sxs-lookup"><span data-stu-id="afa81-813">The extension is not installed.</span></span> <span data-ttu-id="afa81-814">Determine whether this is a proxy issue (as described earlier).</span><span class="sxs-lookup"><span data-stu-id="afa81-814">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="afa81-815">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span><span class="sxs-lookup"><span data-stu-id="afa81-815">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="afa81-817">Some Azure performance counters are missing</span><span class="sxs-lookup"><span data-stu-id="afa81-817">Some Azure performance counters are missing</span></span>
<span data-ttu-id="afa81-818">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span><span class="sxs-lookup"><span data-stu-id="afa81-818">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="afa81-819">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="afa81-819">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="afa81-820">Storage counters come from the logs in your storage subscription.</span><span class="sxs-lookup"><span data-stu-id="afa81-820">Storage counters come from the logs in your storage subscription.</span></span>

<span data-ttu-id="afa81-821">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span><span class="sxs-lookup"><span data-stu-id="afa81-821">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="afa81-822">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="afa81-822">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="afa81-823">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span><span class="sxs-lookup"><span data-stu-id="afa81-823">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="afa81-824">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="afa81-824">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
















































