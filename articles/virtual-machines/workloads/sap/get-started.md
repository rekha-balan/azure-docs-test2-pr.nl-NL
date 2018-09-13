---
title: Getting started with SAP on Azure VMs | Microsoft Docs
description: Learn about SAP solutions running on virtual machines (VMs) in Microsoft Azure
services: virtual-machines-linux
documentationcenter: ''
author: RicksterCDN
manager: timlt
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2cb8a1172573e85647dffe614dedff23adde9fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556376"
---
# <a name="using-sap-on-azure-virtual-machines-vms"></a><span data-ttu-id="a2f16-103">Using SAP on Azure Virtual Machines (VMs)</span><span class="sxs-lookup"><span data-stu-id="a2f16-103">Using SAP on Azure Virtual Machines (VMs)</span></span>
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

[dbms-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

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

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/virtual-machines-shared-sap-shared/Windows.png

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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

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

<span data-ttu-id="a2f16-105">By choosing Microsoft Azure as your SAP ready cloud partner, you are able to reliably run your mission critical SAP workloads on a scaleable, compliant, and enterprise-proven platform.</span><span class="sxs-lookup"><span data-stu-id="a2f16-105">By choosing Microsoft Azure as your SAP ready cloud partner, you are able to reliably run your mission critical SAP workloads on a scaleable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="a2f16-106">Get the scalability, flexibility, and cost savings of Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f16-106">Get the scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="a2f16-107">With the expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in azure - and be fully supported.</span><span class="sxs-lookup"><span data-stu-id="a2f16-107">With the expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in azure - and be fully supported.</span></span> <span data-ttu-id="a2f16-108">From SAP NetWeaver to SAP S4/HANA, Linux to Windows, SAP HANA to SQL, we have you covered.</span><span class="sxs-lookup"><span data-stu-id="a2f16-108">From SAP NetWeaver to SAP S4/HANA, Linux to Windows, SAP HANA to SQL, we have you covered.</span></span> 

<span data-ttu-id="a2f16-109">With Microsoft Azure virtual machine services, and SAP HANA on Azure large instances, Microsoft offers a comprehensive Infrastructure As A Service (IaaS) platform.</span><span class="sxs-lookup"><span data-stu-id="a2f16-109">With Microsoft Azure virtual machine services, and SAP HANA on Azure large instances, Microsoft offers a comprehensive Infrastructure As A Service (IaaS) platform.</span></span> <span data-ttu-id="a2f16-110">Because a wide range of SAP solutions are supported on Azure, this "getting started document" will serve as a Table of Contents for our current set of SAP documents.</span><span class="sxs-lookup"><span data-stu-id="a2f16-110">Because a wide range of SAP solutions are supported on Azure, this "getting started document" will serve as a Table of Contents for our current set of SAP documents.</span></span> <span data-ttu-id="a2f16-111">As more titles get added to our document library - you will see them added here.</span><span class="sxs-lookup"><span data-stu-id="a2f16-111">As more titles get added to our document library - you will see them added here.</span></span> 

## <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="a2f16-112">Getting started with SAP HANA on Azure</span><span class="sxs-lookup"><span data-stu-id="a2f16-112">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="a2f16-113">Title: Quickstart guide for manual installation of SAP HANA on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="a2f16-113">Title: Quickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="a2f16-114">Summary: This quickstart guide will help to set up a single-instance SAP HANA prototype/demo system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span><span class="sxs-lookup"><span data-stu-id="a2f16-114">Summary: This quickstart guide will help to set up a single-instance SAP HANA prototype/demo system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="a2f16-115">The guide presumes that the reader is familiar with Azure IaaS basics like how to deploy virtual machines or virtual networks either via the Azure portal or Powershell/CLI including the option to use json templates.</span><span class="sxs-lookup"><span data-stu-id="a2f16-115">The guide presumes that the reader is familiar with Azure IaaS basics like how to deploy virtual machines or virtual networks either via the Azure portal or Powershell/CLI including the option to use json templates.</span></span> <span data-ttu-id="a2f16-116">Furthermore it's expected that the reader is familiar with SAP HANA, SAP NetWeaver and how to install it on-premises.</span><span class="sxs-lookup"><span data-stu-id="a2f16-116">Furthermore it's expected that the reader is familiar with SAP HANA, SAP NetWeaver and how to install it on-premises.</span></span>

<span data-ttu-id="a2f16-117">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-117">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-118">This guide can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-118">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a2f16-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="a2f16-120">Title: Overview and Architecture of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-120">Title: Overview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a2f16-121">Summary: This Architecture and Technical Deployment Guide provides information to help you deploy SAP on the new SAP HANA on Azure (Large Instances) in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f16-121">Summary: This Architecture and Technical Deployment Guide provides information to help you deploy SAP on the new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="a2f16-122">It is not intended to be a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span><span class="sxs-lookup"><span data-stu-id="a2f16-122">It is not intended to be a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="a2f16-123">It should not replace SAP documentation related to the installation of SAP HANA (or the many SAP Support Notes that cover the topic).</span><span class="sxs-lookup"><span data-stu-id="a2f16-123">It should not replace SAP documentation related to the installation of SAP HANA (or the many SAP Support Notes that cover the topic).</span></span> <span data-ttu-id="a2f16-124">It gives you an overview and provides the additional detail of installing SAP HANA on Azure (Large Instances).</span><span class="sxs-lookup"><span data-stu-id="a2f16-124">It gives you an overview and provides the additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="a2f16-125">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-125">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-126">This guide can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="infrastructure-and-connectivity-to-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a2f16-127">Infrastructure and connectivity to SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-127">Infrastructure and connectivity to SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="a2f16-128">Title: Infrastructure and Connectivity to SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-128">Title: Infrastructure and Connectivity to SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a2f16-129">Summary: After the purchase of SAP HANA on Azure (Large Instances) is finalized between you and the Microsoft enterprise account team, various network configurations are required in order to ensure proper connectivity.</span><span class="sxs-lookup"><span data-stu-id="a2f16-129">Summary: After the purchase of SAP HANA on Azure (Large Instances) is finalized between you and the Microsoft enterprise account team, various network configurations are required in order to ensure proper connectivity.</span></span>  <span data-ttu-id="a2f16-130">This document outlines the information that has to be shared with the following information is required.</span><span class="sxs-lookup"><span data-stu-id="a2f16-130">This document outlines the information that has to be shared with the following information is required.</span></span> <span data-ttu-id="a2f16-131">This document outlines what information has to be collected and what configuration scripts have to be run.</span><span class="sxs-lookup"><span data-stu-id="a2f16-131">This document outlines what information has to be collected and what configuration scripts have to be run.</span></span> 

<span data-ttu-id="a2f16-132">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-132">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-133">This guide can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="install-sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a2f16-134">Install SAP HANA on SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-134">Install SAP HANA on SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="a2f16-135">Title: Install SAP HANA on SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-135">Title: Install SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a2f16-136">Summary: This document outlines the setup procedures for installing SAP HANA on your Azure Large Instance.</span><span class="sxs-lookup"><span data-stu-id="a2f16-136">Summary: This document outlines the setup procedures for installing SAP HANA on your Azure Large Instance.</span></span>

<span data-ttu-id="a2f16-137">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-137">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-138">This guide can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a2f16-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="a2f16-140">Title: High Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-140">Title: High Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a2f16-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span><span class="sxs-lookup"><span data-stu-id="a2f16-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="a2f16-142">It's import to work with SAP, your system integrator, and/or Microsoft to properly architect and implement the right HA/DR strategy for you.</span><span class="sxs-lookup"><span data-stu-id="a2f16-142">It's import to work with SAP, your system integrator, and/or Microsoft to properly architect and implement the right HA/DR strategy for you.</span></span> <span data-ttu-id="a2f16-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific to your environment, must be considered.</span><span class="sxs-lookup"><span data-stu-id="a2f16-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific to your environment, must be considered.</span></span>  <span data-ttu-id="a2f16-144">This document explains your options for enabling your preferred level of HA and DR.</span><span class="sxs-lookup"><span data-stu-id="a2f16-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="a2f16-145">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-145">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-146">This document can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a2f16-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="a2f16-148">Title: Troubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="a2f16-148">Title: Troubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a2f16-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span><span class="sxs-lookup"><span data-stu-id="a2f16-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="a2f16-150">Updated: December 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-150">Updated: December 2016</span></span>

[<span data-ttu-id="a2f16-151">This document can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="a2f16-152">Quickstart guide for NetWeaver on SUSE Linux on Azure</span><span class="sxs-lookup"><span data-stu-id="a2f16-152">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="a2f16-153">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span><span class="sxs-lookup"><span data-stu-id="a2f16-153">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="a2f16-154">Summary: This article describes various things to consider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="a2f16-154">Summary: This article describes various things to consider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="a2f16-155">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f16-155">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="a2f16-156">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span><span class="sxs-lookup"><span data-stu-id="a2f16-156">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="a2f16-157">Updated: September 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-157">Updated: September 2016</span></span>

[<span data-ttu-id="a2f16-158">This guide can be found here</span><span class="sxs-lookup"><span data-stu-id="a2f16-158">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a><span data-ttu-id="a2f16-159">Planning and implementation</span><span class="sxs-lookup"><span data-stu-id="a2f16-159">Planning and implementation</span></span>
<span data-ttu-id="a2f16-160">Title: SAP NetWeaver on Linux virtual machines (VMs) – Planning and Implementation Guide</span><span class="sxs-lookup"><span data-stu-id="a2f16-160">Title: SAP NetWeaver on Linux virtual machines (VMs) – Planning and Implementation Guide</span></span>

<span data-ttu-id="a2f16-161">Summary: This is the paper to start with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="a2f16-161">Summary: This is the paper to start with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="a2f16-162">This planning and implementation guide will help you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed to an Azure Virtual Machines environment.</span><span class="sxs-lookup"><span data-stu-id="a2f16-162">This planning and implementation guide will help you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed to an Azure Virtual Machines environment.</span></span> <span data-ttu-id="a2f16-163">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific to Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f16-163">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific to Azure.</span></span> <span data-ttu-id="a2f16-164">The paper lists and describes all the necessary configuration information you’ll need on the SAP/Azure side to run a hybrid SAP landscape.</span><span class="sxs-lookup"><span data-stu-id="a2f16-164">The paper lists and describes all the necessary configuration information you’ll need on the SAP/Azure side to run a hybrid SAP landscape.</span></span> <span data-ttu-id="a2f16-165">Measures you can take to ensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span><span class="sxs-lookup"><span data-stu-id="a2f16-165">Measures you can take to ensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="a2f16-166">Updated: March 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-166">Updated: March 2016</span></span>

<span data-ttu-id="a2f16-167">[This guide can be found here][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="a2f16-167">[This guide can be found here][planning-guide]</span></span>

## <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a><span data-ttu-id="a2f16-168">Deployment</span><span class="sxs-lookup"><span data-stu-id="a2f16-168">Deployment</span></span>
<span data-ttu-id="a2f16-169">Title: SAP NetWeaver on Linux virtual machines (VMs) – Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="a2f16-169">Title: SAP NetWeaver on Linux virtual machines (VMs) – Deployment Guide</span></span>

<span data-ttu-id="a2f16-170">Summary: This document provides procedural guidance for deploying SAP NetWeaver software to virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f16-170">Summary: This document provides procedural guidance for deploying SAP NetWeaver software to virtual machines in Azure.</span></span> <span data-ttu-id="a2f16-171">This paper focuses on three specific deployment scenarios, with an emphasis on enabling the Azure Monitoring Extensions for SAP, including troubleshooting recommendations for the Azure Monitoring Extensions for SAP.</span><span class="sxs-lookup"><span data-stu-id="a2f16-171">This paper focuses on three specific deployment scenarios, with an emphasis on enabling the Azure Monitoring Extensions for SAP, including troubleshooting recommendations for the Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="a2f16-172">This paper assumes that you’ve read the planning and implementation guide.</span><span class="sxs-lookup"><span data-stu-id="a2f16-172">This paper assumes that you’ve read the planning and implementation guide.</span></span>

<span data-ttu-id="a2f16-173">Updated: March 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-173">Updated: March 2016</span></span>

<span data-ttu-id="a2f16-174">[This guide can be found here][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="a2f16-174">[This guide can be found here][deployment-guide]</span></span>

## <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a><span data-ttu-id="a2f16-175">DBMS deployment guide</span><span class="sxs-lookup"><span data-stu-id="a2f16-175">DBMS deployment guide</span></span>
<span data-ttu-id="a2f16-176">Title: SAP NetWeaver on Linux virtual machines (VMs) – DBMS Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="a2f16-176">Title: SAP NetWeaver on Linux virtual machines (VMs) – DBMS Deployment Guide</span></span>

<span data-ttu-id="a2f16-177">Summary: This paper covers planning and implementation considerations for the DBMS systems that should run in conjunction with SAP.</span><span class="sxs-lookup"><span data-stu-id="a2f16-177">Summary: This paper covers planning and implementation considerations for the DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="a2f16-178">In the first part, general considerations are listed and presented.</span><span class="sxs-lookup"><span data-stu-id="a2f16-178">In the first part, general considerations are listed and presented.</span></span> <span data-ttu-id="a2f16-179">The following parts of the paper relate to deployments of different DBMS in Azure that are supported by SAP.</span><span class="sxs-lookup"><span data-stu-id="a2f16-179">The following parts of the paper relate to deployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="a2f16-180">Different DBMS presented are SQL Server, SAP ASE and Oracle.</span><span class="sxs-lookup"><span data-stu-id="a2f16-180">Different DBMS presented are SQL Server, SAP ASE and Oracle.</span></span> <span data-ttu-id="a2f16-181">In those specific parts considerations you have to account for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span><span class="sxs-lookup"><span data-stu-id="a2f16-181">In those specific parts considerations you have to account for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="a2f16-182">Subjects like backup and high availability methods that are supported by the different DBMS on Azure are presented for the usage with SAP applications.</span><span class="sxs-lookup"><span data-stu-id="a2f16-182">Subjects like backup and high availability methods that are supported by the different DBMS on Azure are presented for the usage with SAP applications.</span></span>

<span data-ttu-id="a2f16-183">Updated: March 2016</span><span class="sxs-lookup"><span data-stu-id="a2f16-183">Updated: March 2016</span></span>

<span data-ttu-id="a2f16-184">[This guide can be found here][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="a2f16-184">[This guide can be found here][dbms-guide]</span></span>

















































