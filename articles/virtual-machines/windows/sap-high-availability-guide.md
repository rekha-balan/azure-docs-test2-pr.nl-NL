---
title: Azure Virtual Machines high availability for SAP NetWeaver | Microsoft Docs
description: High-availability guide for SAP NetWeaver on Azure Virtual Machines
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d53c1de90cef2c0b236c47d55a35d5bb62a3f833
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672222"
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="08aa4-103">High availability for SAP NetWeaver on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="08aa4-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md

[dbms-guide]:../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

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
[deployment-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/sap-get-started.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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

[planning-guide-figure-100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-1]:#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-azure-resource-manager-architecture]:../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
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
[./windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[./windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener]:classic/virtual-machines-windows-classic-ps-sql-int-listener.md
[./windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[./windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener]:sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
[./windows/sql/virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:sql/virtual-machines-windows-sql-high-availability-dr.md
[./windows/sql/virtual-machines-sql-server-infrastructure-services]:sql/virtual-machines-windows-sql-server-iaas-overview.md
[./windows/sql/virtual-machines-sql-server-performance-best-practices]:sql/virtual-machines-windows-sql-performance.md
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


<span data-ttu-id="08aa4-111">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span><span class="sxs-lookup"><span data-stu-id="08aa4-111">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="08aa4-112">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span><span class="sxs-lookup"><span data-stu-id="08aa4-112">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="08aa4-113">Extend reliability and availability without additional on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="08aa4-113">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="08aa4-114">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span><span class="sxs-lookup"><span data-stu-id="08aa4-114">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="08aa4-115">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="08aa4-115">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="08aa4-116">We walk you through these major tasks:</span><span class="sxs-lookup"><span data-stu-id="08aa4-116">We walk you through these major tasks:</span></span>

* <span data-ttu-id="08aa4-117">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span><span class="sxs-lookup"><span data-stu-id="08aa4-117">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="08aa4-118">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span><span class="sxs-lookup"><span data-stu-id="08aa4-118">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="08aa4-119">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="08aa4-119">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="08aa4-120">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-120">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="08aa4-121">Learn about Windows Server Failover Clustering shared storage in Azure services.</span><span class="sxs-lookup"><span data-stu-id="08aa4-121">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="08aa4-122">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-122">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="08aa4-123">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08aa4-123">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="08aa4-124">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-124">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="08aa4-125">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="08aa4-125">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="08aa4-126">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-126">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="08aa4-127">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-127">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> <span data-ttu-id="08aa4-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08aa4-128">Prerequisites</span></span>
<span data-ttu-id="08aa4-129">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="08aa4-129">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="08aa4-130">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span><span class="sxs-lookup"><span data-stu-id="08aa4-130">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="08aa4-131">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="08aa4-131">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="08aa4-132">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="08aa4-132">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> <span data-ttu-id="08aa4-133">Resources</span><span class="sxs-lookup"><span data-stu-id="08aa4-133">Resources</span></span>
<span data-ttu-id="08aa4-134">These articles cover SAP deployments in Azure:</span><span class="sxs-lookup"><span data-stu-id="08aa4-134">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="08aa4-135">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="08aa4-135">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="08aa4-136">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="08aa4-136">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="08aa4-137">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="08aa4-137">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="08aa4-138">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="08aa4-138">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-139">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="08aa4-139">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="08aa4-140">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span><span class="sxs-lookup"><span data-stu-id="08aa4-140">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="08aa4-141">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-141">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="08aa4-142">These SAP Notes are related to the topic of SAP in Azure:</span><span class="sxs-lookup"><span data-stu-id="08aa4-142">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="08aa4-143">Note number</span><span class="sxs-lookup"><span data-stu-id="08aa4-143">Note number</span></span> | <span data-ttu-id="08aa4-144">Title</span><span class="sxs-lookup"><span data-stu-id="08aa4-144">Title</span></span> |
| --- | --- |
| <span data-ttu-id="08aa4-145">[1928533]</span><span class="sxs-lookup"><span data-stu-id="08aa4-145">[1928533]</span></span> |<span data-ttu-id="08aa4-146">SAP Applications on Azure: Supported Products and Sizing</span><span class="sxs-lookup"><span data-stu-id="08aa4-146">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="08aa4-147">[2015553]</span><span class="sxs-lookup"><span data-stu-id="08aa4-147">[2015553]</span></span> |<span data-ttu-id="08aa4-148">SAP on Microsoft Azure: Support Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08aa4-148">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="08aa4-149">[1999351]</span><span class="sxs-lookup"><span data-stu-id="08aa4-149">[1999351]</span></span> |<span data-ttu-id="08aa4-150">Enhanced Azure Monitoring for SAP</span><span class="sxs-lookup"><span data-stu-id="08aa4-150">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="08aa4-151">[2178632]</span><span class="sxs-lookup"><span data-stu-id="08aa4-151">[2178632]</span></span> |<span data-ttu-id="08aa4-152">Key Monitoring Metrics for SAP on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="08aa4-152">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="08aa4-153">[1999351]</span><span class="sxs-lookup"><span data-stu-id="08aa4-153">[1999351]</span></span> |<span data-ttu-id="08aa4-154">Virtualization on Windows: Enhanced Monitoring</span><span class="sxs-lookup"><span data-stu-id="08aa4-154">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="08aa4-155">[2243692]</span><span class="sxs-lookup"><span data-stu-id="08aa4-155">[2243692]</span></span> |<span data-ttu-id="08aa4-156">Use of Azure Premium SSD Storage for SAP DBMS Instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-156">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="08aa4-157">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span><span class="sxs-lookup"><span data-stu-id="08aa4-157">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a><span data-ttu-id="08aa4-158">High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span><span class="sxs-lookup"><span data-stu-id="08aa4-158">High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="08aa4-159">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span><span class="sxs-lookup"><span data-stu-id="08aa4-159">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="08aa4-160">Resource groups</span><span class="sxs-lookup"><span data-stu-id="08aa4-160">Resource groups</span></span>
- <span data-ttu-id="08aa4-161">Azure internal load balancer dependency on the Azure resource group</span><span class="sxs-lookup"><span data-stu-id="08aa4-161">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="08aa4-162">Support for SAP multi-SID scenarios</span><span class="sxs-lookup"><span data-stu-id="08aa4-162">Support for SAP multi-SID scenarios</span></span>

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> <span data-ttu-id="08aa4-163">Resource groups</span><span class="sxs-lookup"><span data-stu-id="08aa4-163">Resource groups</span></span>
<span data-ttu-id="08aa4-164">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="08aa4-164">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="08aa4-165">An integrated approach, in a resource group, all resources have the same life cycle.</span><span class="sxs-lookup"><span data-stu-id="08aa4-165">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="08aa4-166">For example, all resources are created at the same time and they are deleted at the same time.</span><span class="sxs-lookup"><span data-stu-id="08aa4-166">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="08aa4-167">Learn more about [resource groups](../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="08aa4-167">Learn more about [resource groups](../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> <span data-ttu-id="08aa4-168">Azure internal load balancer dependency on the Azure resource group</span><span class="sxs-lookup"><span data-stu-id="08aa4-168">Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="08aa4-169">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service group.</span><span class="sxs-lookup"><span data-stu-id="08aa4-169">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service group.</span></span> <span data-ttu-id="08aa4-170">Every internal load balancer needs one cloud service group.</span><span class="sxs-lookup"><span data-stu-id="08aa4-170">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="08aa4-171">In Azure Resource Manager, you don't need an Azure resource group to use Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-171">In Azure Resource Manager, you don't need an Azure resource group to use Azure Load Balancer.</span></span> <span data-ttu-id="08aa4-172">The environment is simpler and more flexible.</span><span class="sxs-lookup"><span data-stu-id="08aa4-172">The environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="08aa4-173">Support for SAP multi-SID scenarios</span><span class="sxs-lookup"><span data-stu-id="08aa4-173">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="08aa4-174">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-174">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="08aa4-175">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-175">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="08aa4-176">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="08aa4-176">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08aa4-177">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span><span class="sxs-lookup"><span data-stu-id="08aa4-177">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="08aa4-178">It offers many benefits that are not available in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="08aa4-178">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="08aa4-179">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="08aa4-179">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> <span data-ttu-id="08aa4-180">Windows Server Failover Clustering</span><span class="sxs-lookup"><span data-stu-id="08aa4-180">Windows Server Failover Clustering</span></span>
<span data-ttu-id="08aa4-181">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span><span class="sxs-lookup"><span data-stu-id="08aa4-181">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="08aa4-182">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span><span class="sxs-lookup"><span data-stu-id="08aa4-182">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="08aa4-183">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span><span class="sxs-lookup"><span data-stu-id="08aa4-183">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="08aa4-184">You can choose from different quorum modes to achieve failover clustering.</span><span class="sxs-lookup"><span data-stu-id="08aa4-184">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> <span data-ttu-id="08aa4-185">Quorum modes</span><span class="sxs-lookup"><span data-stu-id="08aa4-185">Quorum modes</span></span>
<span data-ttu-id="08aa4-186">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="08aa4-186">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="08aa4-187">**Node Majority**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-187">**Node Majority**.</span></span> <span data-ttu-id="08aa4-188">Each node of the cluster can vote.</span><span class="sxs-lookup"><span data-stu-id="08aa4-188">Each node of the cluster can vote.</span></span> <span data-ttu-id="08aa4-189">The cluster functions only with a majority of votes, that is, with more than half the votes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-189">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="08aa4-190">We recommend this option for clusters that have an uneven number of nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-190">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="08aa4-191">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span><span class="sxs-lookup"><span data-stu-id="08aa4-191">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="08aa4-192">**Node and Disk Majority**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-192">**Node and Disk Majority**.</span></span> <span data-ttu-id="08aa4-193">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span><span class="sxs-lookup"><span data-stu-id="08aa4-193">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="08aa4-194">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-194">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="08aa4-195">This mode makes sense in a cluster environment with an even number of nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-195">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="08aa4-196">If half the nodes and the disk are online, the cluster remains in a healthy state.</span><span class="sxs-lookup"><span data-stu-id="08aa4-196">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="08aa4-197">**Node and File Share Majority**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-197">**Node and File Share Majority**.</span></span> <span data-ttu-id="08aa4-198">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span><span class="sxs-lookup"><span data-stu-id="08aa4-198">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="08aa4-199">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-199">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="08aa4-200">This mode makes sense in a cluster environment with an even number of nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-200">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="08aa4-201">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-201">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="08aa4-202">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-202">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="08aa4-203">**No Majority: Disk Only**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-203">**No Majority: Disk Only**.</span></span> <span data-ttu-id="08aa4-204">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span><span class="sxs-lookup"><span data-stu-id="08aa4-204">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="08aa4-205">Only the nodes that also are in communication with that disk can join the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-205">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="08aa4-206">We recommend that you do not use this mode.</span><span class="sxs-lookup"><span data-stu-id="08aa4-206">We recommend that you do not use this mode.</span></span>
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> <span data-ttu-id="08aa4-207">Windows Server Failover Clustering on-premises</span><span class="sxs-lookup"><span data-stu-id="08aa4-207">Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="08aa4-208">Figure 1 shows a cluster of two nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-208">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="08aa4-209">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span><span class="sxs-lookup"><span data-stu-id="08aa4-209">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="08aa4-210">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span><span class="sxs-lookup"><span data-stu-id="08aa4-210">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="08aa4-211">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span><span class="sxs-lookup"><span data-stu-id="08aa4-211">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="08aa4-212">The Node and Disk Majority also is a valid option.</span><span class="sxs-lookup"><span data-stu-id="08aa4-212">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="08aa4-213">In a production environment, we recommend that you use a quorum disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-213">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="08aa4-214">You can use network and storage system technology to make it highly available.</span><span class="sxs-lookup"><span data-stu-id="08aa4-214">You can use network and storage system technology to make it highly available.</span></span>

![Figure 1: Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="08aa4-216">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span><span class="sxs-lookup"><span data-stu-id="08aa4-216">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> <span data-ttu-id="08aa4-217">Shared storage</span><span class="sxs-lookup"><span data-stu-id="08aa4-217">Shared storage</span></span>
<span data-ttu-id="08aa4-218">Figure 1 also shows a two-node shared storage cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-218">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="08aa4-219">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span><span class="sxs-lookup"><span data-stu-id="08aa4-219">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="08aa4-220">A locking mechanism protects the data from corruption.</span><span class="sxs-lookup"><span data-stu-id="08aa4-220">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="08aa4-221">All nodes can detect if another node fails.</span><span class="sxs-lookup"><span data-stu-id="08aa4-221">All nodes can detect if another node fails.</span></span> <span data-ttu-id="08aa4-222">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span><span class="sxs-lookup"><span data-stu-id="08aa4-222">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-223">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08aa4-223">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="08aa4-224">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-224">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="08aa4-225">In that case, the Windows cluster configuration doesn't need a shared disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-225">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> <span data-ttu-id="08aa4-226">Networking and name resolution</span><span class="sxs-lookup"><span data-stu-id="08aa4-226">Networking and name resolution</span></span>
<span data-ttu-id="08aa4-227">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span><span class="sxs-lookup"><span data-stu-id="08aa4-227">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="08aa4-228">The on-premises nodes and the DNS server can handle multiple IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08aa4-228">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="08aa4-229">In a typical setup, you use two or more network connections:</span><span class="sxs-lookup"><span data-stu-id="08aa4-229">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="08aa4-230">A dedicated connection to the storage</span><span class="sxs-lookup"><span data-stu-id="08aa4-230">A dedicated connection to the storage</span></span>
* <span data-ttu-id="08aa4-231">A cluster-internal network connection for the heartbeat</span><span class="sxs-lookup"><span data-stu-id="08aa4-231">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="08aa4-232">A public network that clients use to connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="08aa4-232">A public network that clients use to connect to the cluster</span></span>

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> <span data-ttu-id="08aa4-233">Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="08aa4-233">Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="08aa4-234">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="08aa4-234">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="08aa4-235">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-235">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="08aa4-236">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-236">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="08aa4-237">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-237">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="08aa4-238">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-238">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Figure 2: Windows Server Failover Clustering configuration in Azure without a shared disk][sap-ha-guide-figure-1001]

<span data-ttu-id="08aa4-240">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span><span class="sxs-lookup"><span data-stu-id="08aa4-240">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> <span data-ttu-id="08aa4-241">Shared disk in Azure with SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="08aa4-241">Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="08aa4-242">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-242">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="08aa4-243">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-243">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="08aa4-244">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span><span class="sxs-lookup"><span data-stu-id="08aa4-244">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="08aa4-245">The SIOS solution provides real-time synchronous data replication.</span><span class="sxs-lookup"><span data-stu-id="08aa4-245">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="08aa4-246">This is how you can create a shared disk resource for a cluster:</span><span class="sxs-lookup"><span data-stu-id="08aa4-246">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="08aa4-247">Attach an additional Azure virtual hard disk (VHD) to each of the virtual machines (VMs) in a Windows cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="08aa4-247">Attach an additional Azure virtual hard disk (VHD) to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="08aa4-248">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-248">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="08aa4-249">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional VHD attached volume from the source virtual machine to the additional VHD attached volume of the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-249">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional VHD attached volume from the source virtual machine to the additional VHD attached volume of the target virtual machine.</span></span> <span data-ttu-id="08aa4-250">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-250">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="08aa4-251">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="08aa4-251">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figure 3: Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="08aa4-253">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="08aa4-253">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-254">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08aa4-254">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="08aa4-255">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-255">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="08aa4-256">In this case, the Windows cluster configuration doesn't need a shared disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-256">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> <span data-ttu-id="08aa4-257">Name resolution in Azure</span><span class="sxs-lookup"><span data-stu-id="08aa4-257">Name resolution in Azure</span></span>
<span data-ttu-id="08aa4-258">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08aa4-258">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="08aa4-259">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span><span class="sxs-lookup"><span data-stu-id="08aa4-259">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="08aa4-260">Azure has an internal load balancer in the Azure Load Balancer service.</span><span class="sxs-lookup"><span data-stu-id="08aa4-260">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="08aa4-261">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span><span class="sxs-lookup"><span data-stu-id="08aa4-261">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="08aa4-262">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-262">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="08aa4-263">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-263">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="08aa4-264">The clients can connect via the virtual host name.</span><span class="sxs-lookup"><span data-stu-id="08aa4-264">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="08aa4-265">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-265">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> <span data-ttu-id="08aa4-266">SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span><span class="sxs-lookup"><span data-stu-id="08aa4-266">SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="08aa4-267">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span><span class="sxs-lookup"><span data-stu-id="08aa4-267">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="08aa4-268">SAP Application Server instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-268">SAP Application Server instance</span></span>
* <span data-ttu-id="08aa4-269">SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-269">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="08aa4-270">DBMS server</span><span class="sxs-lookup"><span data-stu-id="08aa4-270">DBMS server</span></span>

<span data-ttu-id="08aa4-271">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="08aa4-271">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> <span data-ttu-id="08aa4-272">High-availability SAP Application Server</span><span class="sxs-lookup"><span data-stu-id="08aa4-272">High-availability SAP Application Server</span></span>
<span data-ttu-id="08aa4-273">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span><span class="sxs-lookup"><span data-stu-id="08aa4-273">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="08aa4-274">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-274">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="08aa4-275">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-275">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figure 4: High-availability SAP Application Server][sap-ha-guide-figure-2000]

<span data-ttu-id="08aa4-277">_**Figure 4:** High-availability SAP Application Server_</span><span class="sxs-lookup"><span data-stu-id="08aa4-277">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="08aa4-278">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span><span class="sxs-lookup"><span data-stu-id="08aa4-278">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="08aa4-279">An Azure availability set ensures that:</span><span class="sxs-lookup"><span data-stu-id="08aa4-279">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="08aa4-280">All virtual machines are part of the same upgrade domain.</span><span class="sxs-lookup"><span data-stu-id="08aa4-280">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="08aa4-281">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span><span class="sxs-lookup"><span data-stu-id="08aa4-281">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="08aa4-282">All virtual machines are part of the same fault domain.</span><span class="sxs-lookup"><span data-stu-id="08aa4-282">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="08aa4-283">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-283">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="08aa4-284">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="08aa4-284">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="08aa4-285">Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span><span class="sxs-lookup"><span data-stu-id="08aa4-285">Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="08aa4-286">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span><span class="sxs-lookup"><span data-stu-id="08aa4-286">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> <span data-ttu-id="08aa4-287">High-availability SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-287">High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="08aa4-288">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-288">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figure 5: High-availability SAP ASCS/SCS instance][sap-ha-guide-figure-2001]

<span data-ttu-id="08aa4-290">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span><span class="sxs-lookup"><span data-stu-id="08aa4-290">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> <span data-ttu-id="08aa4-291">SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span><span class="sxs-lookup"><span data-stu-id="08aa4-291">SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="08aa4-292">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="08aa4-292">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="08aa4-293">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-293">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="08aa4-294">We discuss this in more detail later in the article.</span><span class="sxs-lookup"><span data-stu-id="08aa4-294">We discuss this in more detail later in the article.</span></span>

![Figure 6: Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure by using SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="08aa4-296">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="08aa4-296">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a><span data-ttu-id="08aa4-297">High-availability DBMS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-297">High-availability DBMS instance</span></span>
<span data-ttu-id="08aa4-298">The DBMS also is a single point of contact in an SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-298">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="08aa4-299">You need to protect it by using a high-availability solution.</span><span class="sxs-lookup"><span data-stu-id="08aa4-299">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="08aa4-300">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-300">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="08aa4-301">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span><span class="sxs-lookup"><span data-stu-id="08aa4-301">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="08aa4-302">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span><span class="sxs-lookup"><span data-stu-id="08aa4-302">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Figure 7: Example of a high-availability SAP DBMS, with SQL Server Always On][sap-ha-guide-figure-2003]

<span data-ttu-id="08aa4-304">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span><span class="sxs-lookup"><span data-stu-id="08aa4-304">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="08aa4-305">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span><span class="sxs-lookup"><span data-stu-id="08aa4-305">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="08aa4-306">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="08aa4-306">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="08aa4-307">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="08aa4-307">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> <span data-ttu-id="08aa4-308">End-to-end high-availability deployment scenarios</span><span class="sxs-lookup"><span data-stu-id="08aa4-308">End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="08aa4-309">Deployment scenario using Architectural Template 1</span><span class="sxs-lookup"><span data-stu-id="08aa4-309">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="08aa4-310">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-310">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="08aa4-311">This scenario is set up as follows:</span><span class="sxs-lookup"><span data-stu-id="08aa4-311">This scenario is set up as follows:</span></span>

- <span data-ttu-id="08aa4-312">One dedicated cluster is used for the SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-312">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="08aa4-313">One dedicated cluster is used for the DBMS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-313">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="08aa4-314">SAP Application Server instances are deployed in their own dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="08aa4-314">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figure 8: SAP high-availability Architectural Template 1, with dedicated cluster for ASCS/SCS and DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="08aa4-316">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span><span class="sxs-lookup"><span data-stu-id="08aa4-316">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="08aa4-317">Deployment scenario using Architectural Template 2</span><span class="sxs-lookup"><span data-stu-id="08aa4-317">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="08aa4-318">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-318">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="08aa4-319">This scenario is set up as follows:</span><span class="sxs-lookup"><span data-stu-id="08aa4-319">This scenario is set up as follows:</span></span>

- <span data-ttu-id="08aa4-320">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span><span class="sxs-lookup"><span data-stu-id="08aa4-320">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="08aa4-321">SAP Application Server instances are deployed in own dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="08aa4-321">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figure 9: SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="08aa4-323">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span><span class="sxs-lookup"><span data-stu-id="08aa4-323">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="08aa4-324">Deployment scenario using Architectural Template 3</span><span class="sxs-lookup"><span data-stu-id="08aa4-324">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="08aa4-325">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="08aa4-325">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="08aa4-326">This scenario is set up as follows:</span><span class="sxs-lookup"><span data-stu-id="08aa4-326">This scenario is set up as follows:</span></span>

- <span data-ttu-id="08aa4-327">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span><span class="sxs-lookup"><span data-stu-id="08aa4-327">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="08aa4-328">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span><span class="sxs-lookup"><span data-stu-id="08aa4-328">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="08aa4-329">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="08aa4-329">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="08aa4-330">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="08aa4-330">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Figure 10: SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances][sap-ha-guide-figure-6003]

<span data-ttu-id="08aa4-332">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span><span class="sxs-lookup"><span data-stu-id="08aa4-332">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> <span data-ttu-id="08aa4-333">Prepare the infrastructure</span><span class="sxs-lookup"><span data-stu-id="08aa4-333">Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="08aa4-334">Prepare the infrastructure for Architectural Template 1</span><span class="sxs-lookup"><span data-stu-id="08aa4-334">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="08aa4-335">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span><span class="sxs-lookup"><span data-stu-id="08aa4-335">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="08aa4-336">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span><span class="sxs-lookup"><span data-stu-id="08aa4-336">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="08aa4-337">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span><span class="sxs-lookup"><span data-stu-id="08aa4-337">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="08aa4-338">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span><span class="sxs-lookup"><span data-stu-id="08aa4-338">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="08aa4-339">Azure Marketplace image</span><span class="sxs-lookup"><span data-stu-id="08aa4-339">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="08aa4-340">Custom image</span><span class="sxs-lookup"><span data-stu-id="08aa4-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="08aa4-341">To prepare the infrastructure for Architectural Template 1:</span><span class="sxs-lookup"><span data-stu-id="08aa4-341">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="08aa4-342">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-342">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figure 11: Set SAP high-availability Azure Resource Manager parameters][sap-ha-guide-figure-3000]

<span data-ttu-id="08aa4-344">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span><span class="sxs-lookup"><span data-stu-id="08aa4-344">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="08aa4-345">The templates create:</span><span class="sxs-lookup"><span data-stu-id="08aa4-345">The templates create:</span></span>

  * <span data-ttu-id="08aa4-346">**Virtual machines**:</span><span class="sxs-lookup"><span data-stu-id="08aa4-346">**Virtual machines**:</span></span>
    * <span data-ttu-id="08aa4-347">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-347">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="08aa4-348">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-348">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="08aa4-349">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-349">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="08aa4-350">**Network cards for all virtual machines, with associated IP addresses**:</span><span class="sxs-lookup"><span data-stu-id="08aa4-350">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="08aa4-351"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-351"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="08aa4-352"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-352"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="08aa4-353"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="08aa4-353"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="08aa4-354">**Azure storage accounts**</span><span class="sxs-lookup"><span data-stu-id="08aa4-354">**Azure storage accounts**</span></span>

  * <span data-ttu-id="08aa4-355">**Availability groups** for:</span><span class="sxs-lookup"><span data-stu-id="08aa4-355">**Availability groups** for:</span></span>
    * <span data-ttu-id="08aa4-356">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="08aa4-356">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="08aa4-357">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="08aa4-357">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="08aa4-358">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="08aa4-358">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="08aa4-359">**Azure internal load balancer**:</span><span class="sxs-lookup"><span data-stu-id="08aa4-359">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="08aa4-360">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="08aa4-360">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="08aa4-361">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span><span class="sxs-lookup"><span data-stu-id="08aa4-361">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="08aa4-362">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-362">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="08aa4-363">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span><span class="sxs-lookup"><span data-stu-id="08aa4-363">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-364">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span><span class="sxs-lookup"><span data-stu-id="08aa4-364">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="08aa4-365">Change them to **static** IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08aa4-365">Change them to **static** IP addresses.</span></span> <span data-ttu-id="08aa4-366">We describe how to do this later in the article.</span><span class="sxs-lookup"><span data-stu-id="08aa4-366">We describe how to do this later in the article.</span></span>
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> <span data-ttu-id="08aa4-367">Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span><span class="sxs-lookup"><span data-stu-id="08aa4-367">Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="08aa4-368">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="08aa4-368">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-369">You can use your Azure Virtual Network instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-369">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="08aa4-370">The virtual network and subnet have already been created and prepared.</span><span class="sxs-lookup"><span data-stu-id="08aa4-370">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="08aa4-371">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-371">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="08aa4-372">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-372">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="08aa4-373">To get a list of all Azure network subnets, run this PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="08aa4-373">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="08aa4-374">The **ID** field shows the **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-374">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="08aa4-375">To get a list of all **SUBNETID** values, run this PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="08aa4-375">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="08aa4-376">The **SUBNETID** looks like this:</span><span class="sxs-lookup"><span data-stu-id="08aa4-376">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> <span data-ttu-id="08aa4-377">Deploy cloud-only SAP instances for test and demo</span><span class="sxs-lookup"><span data-stu-id="08aa4-377">Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="08aa4-378">You can deploy your high-availability SAP system in a cloud-only deployment model.</span><span class="sxs-lookup"><span data-stu-id="08aa4-378">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="08aa4-379">This kind of deployment primarily is useful for demo and test use cases.</span><span class="sxs-lookup"><span data-stu-id="08aa4-379">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="08aa4-380">It's not suited for production use cases.</span><span class="sxs-lookup"><span data-stu-id="08aa4-380">It's not suited for production use cases.</span></span>

- <span data-ttu-id="08aa4-381">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-381">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="08aa4-382">Leave the **SUBNETID** field empty.</span><span class="sxs-lookup"><span data-stu-id="08aa4-382">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="08aa4-383">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="08aa4-383">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-384">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-384">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="08aa4-385">The template doesn't create these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-385">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="08aa4-386">Prepare the infrastructure for Architectural Template 2</span><span class="sxs-lookup"><span data-stu-id="08aa4-386">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="08aa4-387">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span><span class="sxs-lookup"><span data-stu-id="08aa4-387">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="08aa4-388">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span><span class="sxs-lookup"><span data-stu-id="08aa4-388">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="08aa4-389">Azure Marketplace image</span><span class="sxs-lookup"><span data-stu-id="08aa4-389">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="08aa4-390">Custom image</span><span class="sxs-lookup"><span data-stu-id="08aa4-390">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="08aa4-391">Prepare the infrastructure for Architectural Template 3</span><span class="sxs-lookup"><span data-stu-id="08aa4-391">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="08aa4-392">You can prepare the infrastructure and configure SAP for **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-392">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="08aa4-393">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="08aa4-393">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="08aa4-394">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="08aa4-394">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="08aa4-395">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="08aa4-395">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="08aa4-396">To create a new multi-SID cluster, you need to deploy the following three templates:</span><span class="sxs-lookup"><span data-stu-id="08aa4-396">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="08aa4-397">ASCS/SCS template</span><span class="sxs-lookup"><span data-stu-id="08aa4-397">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="08aa4-398">Database template</span><span class="sxs-lookup"><span data-stu-id="08aa4-398">Database template</span></span>](#database-template)
* [<span data-ttu-id="08aa4-399">Application servers template</span><span class="sxs-lookup"><span data-stu-id="08aa4-399">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="08aa4-400">The following sections have more details about the templates and the parameters you need to provide in the templates.</span><span class="sxs-lookup"><span data-stu-id="08aa4-400">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <a name="ASCS-SCS-template"></a> <span data-ttu-id="08aa4-401">ASCS/SCS template</span><span class="sxs-lookup"><span data-stu-id="08aa4-401">ASCS/SCS template</span></span>

<span data-ttu-id="08aa4-402">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span><span class="sxs-lookup"><span data-stu-id="08aa4-402">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="08aa4-403">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for the following parameters:</span><span class="sxs-lookup"><span data-stu-id="08aa4-403">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for the following parameters:</span></span>

  - <span data-ttu-id="08aa4-404">**Resource Prefix**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-404">**Resource Prefix**.</span></span>  <span data-ttu-id="08aa4-405">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-405">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="08aa4-406">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-406">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="08aa4-407">The prefix must be between **three and six characters**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-407">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="08aa4-408">**Stack Type**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-408">**Stack Type**.</span></span> <span data-ttu-id="08aa4-409">Select the stack type of the SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-409">Select the stack type of the SAP system.</span></span> <span data-ttu-id="08aa4-410">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-410">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="08aa4-411">**OS Type**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-411">**OS Type**.</span></span> <span data-ttu-id="08aa4-412">Select the operating system of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-412">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="08aa4-413">**SAP System Count**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-413">**SAP System Count**.</span></span> <span data-ttu-id="08aa4-414">Select the number of SAP systems you want to install in this cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-414">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="08aa4-415">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-415">**System Availability**.</span></span> <span data-ttu-id="08aa4-416">Select **HA**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-416">Select **HA**.</span></span>
  -  <span data-ttu-id="08aa4-417">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-417">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="08aa4-418">Create a new user that can be used to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-418">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="08aa4-419">**New Or Existing Subnet**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-419">**New Or Existing Subnet**.</span></span> <span data-ttu-id="08aa4-420">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span><span class="sxs-lookup"><span data-stu-id="08aa4-420">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="08aa4-421">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-421">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="08aa4-422">**Subnet Id**. Set the ID of the subnet to which the virtual machines should be connected.</span><span class="sxs-lookup"><span data-stu-id="08aa4-422">**Subnet Id**. Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="08aa4-423">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="08aa4-423">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="08aa4-424">The ID usually looks like this:</span><span class="sxs-lookup"><span data-stu-id="08aa4-424">The ID usually looks like this:</span></span>

   <span data-ttu-id="08aa4-425">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span><span class="sxs-lookup"><span data-stu-id="08aa4-425">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="08aa4-426">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span><span class="sxs-lookup"><span data-stu-id="08aa4-426">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="08aa4-427">The ASCS instances are configured for instance number 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="08aa4-427">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="08aa4-428">The SCS instances are configured for instance number 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="08aa4-428">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="08aa4-429">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="08aa4-429">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="08aa4-430">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="08aa4-430">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="08aa4-431">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span><span class="sxs-lookup"><span data-stu-id="08aa4-431">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="08aa4-432">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="08aa4-432">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="08aa4-433">Windows-specific ports for every SAP system: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="08aa4-433">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="08aa4-434">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="08aa4-434">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="08aa4-435">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="08aa4-435">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="08aa4-436">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="08aa4-436">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="08aa4-437">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="08aa4-437">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="08aa4-438">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="08aa4-438">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="08aa4-439">ASCS/SCS internal load balancer probe port: 620x0</span><span class="sxs-lookup"><span data-stu-id="08aa4-439">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="08aa4-440">ERS internal load balancer probe port (Linux only): 621x2</span><span class="sxs-lookup"><span data-stu-id="08aa4-440">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <a name="database-template"></a> <span data-ttu-id="08aa4-441">Database template</span><span class="sxs-lookup"><span data-stu-id="08aa4-441">Database template</span></span>

<span data-ttu-id="08aa4-442">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-442">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="08aa4-443">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span><span class="sxs-lookup"><span data-stu-id="08aa4-443">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="08aa4-444">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for the following parameters:</span><span class="sxs-lookup"><span data-stu-id="08aa4-444">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="08aa4-445">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span><span class="sxs-lookup"><span data-stu-id="08aa4-445">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="08aa4-446">The ID will be used as a prefix for the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="08aa4-446">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="08aa4-447">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-447">**Os Type**.</span></span> <span data-ttu-id="08aa4-448">Select the operating system of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-448">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="08aa4-449">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-449">**Dbtype**.</span></span> <span data-ttu-id="08aa4-450">Select the type of the database you want to install on the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-450">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="08aa4-451">Select **SQL** if you want to install Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08aa4-451">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="08aa4-452">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-452">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="08aa4-453">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span><span class="sxs-lookup"><span data-stu-id="08aa4-453">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="08aa4-454">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span><span class="sxs-lookup"><span data-stu-id="08aa4-454">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="08aa4-455">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-455">**SQL**.</span></span> <span data-ttu-id="08aa4-456">The load balancer will load-balance port 1433.</span><span class="sxs-lookup"><span data-stu-id="08aa4-456">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="08aa4-457">Make sure to use this port for your SQL Server Always On setup.</span><span class="sxs-lookup"><span data-stu-id="08aa4-457">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="08aa4-458">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-458">**HANA**.</span></span> <span data-ttu-id="08aa4-459">The load balancer will load-balance ports 35015 and 35017.</span><span class="sxs-lookup"><span data-stu-id="08aa4-459">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="08aa4-460">Make sure to install SAP HANA with instance number **50**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-460">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="08aa4-461">The load balancer will use probe port 62550.</span><span class="sxs-lookup"><span data-stu-id="08aa4-461">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="08aa4-462">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-462">**Sap System Size**.</span></span> <span data-ttu-id="08aa4-463">Set the number of SAPS the new system will provide.</span><span class="sxs-lookup"><span data-stu-id="08aa4-463">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="08aa4-464">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="08aa4-464">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="08aa4-465">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-465">**System Availability**.</span></span> <span data-ttu-id="08aa4-466">Select **HA**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-466">Select **HA**.</span></span>
  -  <span data-ttu-id="08aa4-467">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-467">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="08aa4-468">Create a new user that can be used to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-468">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="08aa4-469">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-469">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <a name="application-servers-template"></a> <span data-ttu-id="08aa4-470">Application servers template</span><span class="sxs-lookup"><span data-stu-id="08aa4-470">Application servers template</span></span>

<span data-ttu-id="08aa4-471">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-471">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="08aa4-472">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span><span class="sxs-lookup"><span data-stu-id="08aa4-472">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="08aa4-473">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for the following parameters:</span><span class="sxs-lookup"><span data-stu-id="08aa4-473">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="08aa4-474">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span><span class="sxs-lookup"><span data-stu-id="08aa4-474">**Sap System Id**. Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="08aa4-475">The ID will be used as a prefix for the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="08aa4-475">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="08aa4-476">**Os Type**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-476">**Os Type**.</span></span> <span data-ttu-id="08aa4-477">Select the operating system of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-477">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="08aa4-478">**Sap System Size**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-478">**Sap System Size**.</span></span> <span data-ttu-id="08aa4-479">The number of SAPS the new system will provide.</span><span class="sxs-lookup"><span data-stu-id="08aa4-479">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="08aa4-480">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span><span class="sxs-lookup"><span data-stu-id="08aa4-480">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="08aa4-481">**System Availability**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-481">**System Availability**.</span></span> <span data-ttu-id="08aa4-482">Select **HA**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-482">Select **HA**.</span></span>
  -  <span data-ttu-id="08aa4-483">**Admin Username and Admin Password**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-483">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="08aa4-484">Create a new user that can be used to sign in to the machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-484">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="08aa4-485">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-485">**Subnet Id**. Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> <span data-ttu-id="08aa4-486">Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="08aa4-486">Azure virtual network</span></span>
<span data-ttu-id="08aa4-487">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="08aa4-487">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="08aa4-488">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="08aa4-488">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="08aa4-489">All virtual machines and internal load balancers are deployed in this virtual network.</span><span class="sxs-lookup"><span data-stu-id="08aa4-489">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08aa4-490">Don't make any changes to the network settings inside the guest operating system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-490">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="08aa4-491">This includes IP addresses, DNS servers, and subnet.</span><span class="sxs-lookup"><span data-stu-id="08aa4-491">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="08aa4-492">Configure all your network settings in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-492">Configure all your network settings in Azure.</span></span> <span data-ttu-id="08aa4-493">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span><span class="sxs-lookup"><span data-stu-id="08aa4-493">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> <span data-ttu-id="08aa4-494">DNS IP addresses</span><span class="sxs-lookup"><span data-stu-id="08aa4-494">DNS IP addresses</span></span>

<span data-ttu-id="08aa4-495">To set the required DNS IP addresses, do the following steps.</span><span class="sxs-lookup"><span data-stu-id="08aa4-495">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="08aa4-496">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-496">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="08aa4-497">Select your settings based on the type of network you have.</span><span class="sxs-lookup"><span data-stu-id="08aa4-497">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="08aa4-498">For more information, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="08aa4-498">For more information, see the following resources:</span></span>
    * <span data-ttu-id="08aa4-499">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span><span class="sxs-lookup"><span data-stu-id="08aa4-499">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="08aa4-500">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-500">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="08aa4-501">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span><span class="sxs-lookup"><span data-stu-id="08aa4-501">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="08aa4-502">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span><span class="sxs-lookup"><span data-stu-id="08aa4-502">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="08aa4-503">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span><span class="sxs-lookup"><span data-stu-id="08aa4-503">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Figure 12: Configure DNS servers for Azure Virtual Network][sap-ha-guide-figure-3001]

    <span data-ttu-id="08aa4-505">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span><span class="sxs-lookup"><span data-stu-id="08aa4-505">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="08aa4-506">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span><span class="sxs-lookup"><span data-stu-id="08aa4-506">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="08aa4-507">In our example, the DNS service is installed and configured on these Windows virtual machines:</span><span class="sxs-lookup"><span data-stu-id="08aa4-507">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="08aa4-508">Virtual machine role</span><span class="sxs-lookup"><span data-stu-id="08aa4-508">Virtual machine role</span></span> | <span data-ttu-id="08aa4-509">Virtual machine host name</span><span class="sxs-lookup"><span data-stu-id="08aa4-509">Virtual machine host name</span></span> | <span data-ttu-id="08aa4-510">Network card name</span><span class="sxs-lookup"><span data-stu-id="08aa4-510">Network card name</span></span> | <span data-ttu-id="08aa4-511">Static IP address</span><span class="sxs-lookup"><span data-stu-id="08aa4-511">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08aa4-512">First DNS server</span><span class="sxs-lookup"><span data-stu-id="08aa4-512">First DNS server</span></span> |<span data-ttu-id="08aa4-513">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-513">domcontr-0</span></span> |<span data-ttu-id="08aa4-514">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-514">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="08aa4-515">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="08aa4-515">10.0.0.10</span></span> |
| <span data-ttu-id="08aa4-516">Second DNS server</span><span class="sxs-lookup"><span data-stu-id="08aa4-516">Second DNS server</span></span> |<span data-ttu-id="08aa4-517">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-517">domcontr-1</span></span> |<span data-ttu-id="08aa4-518">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-518">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="08aa4-519">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="08aa4-519">10.0.0.11</span></span> |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> <span data-ttu-id="08aa4-520">Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-520">Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="08aa4-521">For on-premises deployment, you need these reserved host names and IP addresses:</span><span class="sxs-lookup"><span data-stu-id="08aa4-521">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="08aa4-522">Virtual host name role</span><span class="sxs-lookup"><span data-stu-id="08aa4-522">Virtual host name role</span></span> | <span data-ttu-id="08aa4-523">Virtual host name</span><span class="sxs-lookup"><span data-stu-id="08aa4-523">Virtual host name</span></span> | <span data-ttu-id="08aa4-524">Virtual static IP address</span><span class="sxs-lookup"><span data-stu-id="08aa4-524">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa4-525">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span><span class="sxs-lookup"><span data-stu-id="08aa4-525">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="08aa4-526">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="08aa4-526">pr1-ascs-vir</span></span> |<span data-ttu-id="08aa4-527">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="08aa4-527">10.0.0.42</span></span> |
| <span data-ttu-id="08aa4-528">SAP ASCS/SCS instance virtual host name</span><span class="sxs-lookup"><span data-stu-id="08aa4-528">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="08aa4-529">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="08aa4-529">pr1-ascs-sap</span></span> |<span data-ttu-id="08aa4-530">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="08aa4-530">10.0.0.43</span></span> |
| <span data-ttu-id="08aa4-531">SAP DBMS second cluster virtual host name (cluster management)</span><span class="sxs-lookup"><span data-stu-id="08aa4-531">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="08aa4-532">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="08aa4-532">pr1-dbms-vir</span></span> |<span data-ttu-id="08aa4-533">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="08aa4-533">10.0.0.32</span></span> |

<span data-ttu-id="08aa4-534">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span><span class="sxs-lookup"><span data-stu-id="08aa4-534">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="08aa4-535">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="08aa4-535">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="08aa4-536">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span><span class="sxs-lookup"><span data-stu-id="08aa4-536">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="08aa4-537">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span><span class="sxs-lookup"><span data-stu-id="08aa4-537">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="08aa4-538">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="08aa4-538">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> <span data-ttu-id="08aa4-539">Set static IP addresses for the SAP virtual machines</span><span class="sxs-lookup"><span data-stu-id="08aa4-539">Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="08aa4-540">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-540">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="08aa4-541">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-541">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="08aa4-542">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-542">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="08aa4-543">On the **IP addresses** blade, under **Assignment**, select **Static**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-543">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="08aa4-544">In the **IP address** box, enter the IP address that you want to use.</span><span class="sxs-lookup"><span data-stu-id="08aa4-544">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08aa4-545">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span><span class="sxs-lookup"><span data-stu-id="08aa4-545">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Figure 13: Set static IP addresses for the network card of each virtual machine][sap-ha-guide-figure-3002]

  <span data-ttu-id="08aa4-547">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span><span class="sxs-lookup"><span data-stu-id="08aa4-547">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="08aa4-548">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span><span class="sxs-lookup"><span data-stu-id="08aa4-548">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="08aa4-549">In our example, we have these virtual machines and static IP addresses:</span><span class="sxs-lookup"><span data-stu-id="08aa4-549">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="08aa4-550">Virtual machine role</span><span class="sxs-lookup"><span data-stu-id="08aa4-550">Virtual machine role</span></span> | <span data-ttu-id="08aa4-551">Virtual machine host name</span><span class="sxs-lookup"><span data-stu-id="08aa4-551">Virtual machine host name</span></span> | <span data-ttu-id="08aa4-552">Network card name</span><span class="sxs-lookup"><span data-stu-id="08aa4-552">Network card name</span></span> | <span data-ttu-id="08aa4-553">Static IP address</span><span class="sxs-lookup"><span data-stu-id="08aa4-553">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08aa4-554">First SAP Application Server instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-554">First SAP Application Server instance</span></span> |<span data-ttu-id="08aa4-555">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-555">pr1-di-0</span></span> |<span data-ttu-id="08aa4-556">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-556">pr1-nic-di-0</span></span> |<span data-ttu-id="08aa4-557">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="08aa4-557">10.0.0.50</span></span> |
| <span data-ttu-id="08aa4-558">Second SAP Application Server instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-558">Second SAP Application Server instance</span></span> |<span data-ttu-id="08aa4-559">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-559">pr1-di-1</span></span> |<span data-ttu-id="08aa4-560">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-560">pr1-nic-di-1</span></span> |<span data-ttu-id="08aa4-561">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="08aa4-561">10.0.0.51</span></span> |
| <span data-ttu-id="08aa4-562">...</span><span class="sxs-lookup"><span data-stu-id="08aa4-562">...</span></span> |<span data-ttu-id="08aa4-563">...</span><span class="sxs-lookup"><span data-stu-id="08aa4-563">...</span></span> |<span data-ttu-id="08aa4-564">...</span><span class="sxs-lookup"><span data-stu-id="08aa4-564">...</span></span> |<span data-ttu-id="08aa4-565">...</span><span class="sxs-lookup"><span data-stu-id="08aa4-565">...</span></span> |
| <span data-ttu-id="08aa4-566">Last SAP Application Server instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-566">Last SAP Application Server instance</span></span> |<span data-ttu-id="08aa4-567">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="08aa4-567">pr1-di-5</span></span> |<span data-ttu-id="08aa4-568">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="08aa4-568">pr1-nic-di-5</span></span> |<span data-ttu-id="08aa4-569">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="08aa4-569">10.0.0.55</span></span> |
| <span data-ttu-id="08aa4-570">First cluster node for ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-570">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="08aa4-571">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-571">pr1-ascs-0</span></span> |<span data-ttu-id="08aa4-572">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-572">pr1-nic-ascs-0</span></span> |<span data-ttu-id="08aa4-573">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="08aa4-573">10.0.0.40</span></span> |
| <span data-ttu-id="08aa4-574">Second cluster node for ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-574">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="08aa4-575">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-575">pr1-ascs-1</span></span> |<span data-ttu-id="08aa4-576">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-576">pr1-nic-ascs-1</span></span> |<span data-ttu-id="08aa4-577">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="08aa4-577">10.0.0.41</span></span> |
| <span data-ttu-id="08aa4-578">First cluster node for DBMS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-578">First cluster node for DBMS instance</span></span> |<span data-ttu-id="08aa4-579">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-579">pr1-db-0</span></span> |<span data-ttu-id="08aa4-580">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="08aa4-580">pr1-nic-db-0</span></span> |<span data-ttu-id="08aa4-581">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="08aa4-581">10.0.0.30</span></span> |
| <span data-ttu-id="08aa4-582">Second cluster node for DBMS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-582">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="08aa4-583">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-583">pr1-db-1</span></span> |<span data-ttu-id="08aa4-584">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="08aa4-584">pr1-nic-db-1</span></span> |<span data-ttu-id="08aa4-585">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="08aa4-585">10.0.0.31</span></span> |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> <span data-ttu-id="08aa4-586">Set a static IP address for the Azure internal load balancer</span><span class="sxs-lookup"><span data-stu-id="08aa4-586">Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="08aa4-587">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-587">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08aa4-588">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-588">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="08aa4-589">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-589">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="08aa4-590">To set a static IP address for the Azure internal load balancer:</span><span class="sxs-lookup"><span data-stu-id="08aa4-590">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="08aa4-591">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-591">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="08aa4-592">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-592">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="08aa4-593">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-593">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="08aa4-594">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-594">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Figure 14: Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance][sap-ha-guide-figure-3003]

  <span data-ttu-id="08aa4-596">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span><span class="sxs-lookup"><span data-stu-id="08aa4-596">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="08aa4-597">In our example, we have two Azure internal load balancers that have these static IP addresses:</span><span class="sxs-lookup"><span data-stu-id="08aa4-597">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="08aa4-598">Azure internal load balancer role</span><span class="sxs-lookup"><span data-stu-id="08aa4-598">Azure internal load balancer role</span></span> | <span data-ttu-id="08aa4-599">Azure internal load balancer name</span><span class="sxs-lookup"><span data-stu-id="08aa4-599">Azure internal load balancer name</span></span> | <span data-ttu-id="08aa4-600">Static IP address</span><span class="sxs-lookup"><span data-stu-id="08aa4-600">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa4-601">SAP ASCS/SCS instance internal load balancer</span><span class="sxs-lookup"><span data-stu-id="08aa4-601">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="08aa4-602">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="08aa4-602">pr1-lb-ascs</span></span> |<span data-ttu-id="08aa4-603">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="08aa4-603">10.0.0.43</span></span> |
| <span data-ttu-id="08aa4-604">SAP DBMS internal load balancer</span><span class="sxs-lookup"><span data-stu-id="08aa4-604">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="08aa4-605">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="08aa4-605">pr1-lb-dbms</span></span> |<span data-ttu-id="08aa4-606">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="08aa4-606">10.0.0.33</span></span> |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> <span data-ttu-id="08aa4-607">Default ASCS/SCS load balancing rules for the Azure internal load balancer</span><span class="sxs-lookup"><span data-stu-id="08aa4-607">Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="08aa4-608">The SAP Azure Resource Manager template creates the ports you need:</span><span class="sxs-lookup"><span data-stu-id="08aa4-608">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="08aa4-609">An ABAP ASCS instance, with the default instance number **00**</span><span class="sxs-lookup"><span data-stu-id="08aa4-609">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="08aa4-610">A Java SCS instance, with the default instance number **01**</span><span class="sxs-lookup"><span data-stu-id="08aa4-610">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="08aa4-611">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-611">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="08aa4-612">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span><span class="sxs-lookup"><span data-stu-id="08aa4-612">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="08aa4-613">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span><span class="sxs-lookup"><span data-stu-id="08aa4-613">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="08aa4-614">Service/load balancing rule name</span><span class="sxs-lookup"><span data-stu-id="08aa4-614">Service/load balancing rule name</span></span> | <span data-ttu-id="08aa4-615">Default port numbers</span><span class="sxs-lookup"><span data-stu-id="08aa4-615">Default port numbers</span></span> | <span data-ttu-id="08aa4-616">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span><span class="sxs-lookup"><span data-stu-id="08aa4-616">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa4-617">Enqueue Server / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="08aa4-617">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="08aa4-618">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-618">32<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-619">3200</span><span class="sxs-lookup"><span data-stu-id="08aa4-619">3200</span></span> |
| <span data-ttu-id="08aa4-620">ABAP Message Server / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="08aa4-620">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="08aa4-621">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-621">36<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-622">3600</span><span class="sxs-lookup"><span data-stu-id="08aa4-622">3600</span></span> |
| <span data-ttu-id="08aa4-623">Internal ABAP Message / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="08aa4-623">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="08aa4-624">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-624">39<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-625">3900</span><span class="sxs-lookup"><span data-stu-id="08aa4-625">3900</span></span> |
| <span data-ttu-id="08aa4-626">Message Server HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="08aa4-626">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="08aa4-627">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-627">81<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-628">8100</span><span class="sxs-lookup"><span data-stu-id="08aa4-628">8100</span></span> |
| <span data-ttu-id="08aa4-629">SAP Start Service ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="08aa4-629">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="08aa4-630">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="08aa4-630">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="08aa4-631">50013</span><span class="sxs-lookup"><span data-stu-id="08aa4-631">50013</span></span> |
| <span data-ttu-id="08aa4-632">SAP Start Service ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="08aa4-632">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="08aa4-633">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="08aa4-633">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="08aa4-634">50014</span><span class="sxs-lookup"><span data-stu-id="08aa4-634">50014</span></span> |
| <span data-ttu-id="08aa4-635">Enqueue Replication / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="08aa4-635">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="08aa4-636">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="08aa4-636">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="08aa4-637">50016</span><span class="sxs-lookup"><span data-stu-id="08aa4-637">50016</span></span> |
| <span data-ttu-id="08aa4-638">SAP Start Service ERS HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="08aa4-638">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="08aa4-639">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="08aa4-639">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="08aa4-640">51013</span><span class="sxs-lookup"><span data-stu-id="08aa4-640">51013</span></span> |
| <span data-ttu-id="08aa4-641">SAP Start Service ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="08aa4-641">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="08aa4-642">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="08aa4-642">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="08aa4-643">51014</span><span class="sxs-lookup"><span data-stu-id="08aa4-643">51014</span></span> |
| <span data-ttu-id="08aa4-644">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="08aa4-644">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="08aa4-645">5985</span><span class="sxs-lookup"><span data-stu-id="08aa4-645">5985</span></span> |
| <span data-ttu-id="08aa4-646">File Share *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="08aa4-646">File Share *Lbrule445*</span></span> | |<span data-ttu-id="08aa4-647">445</span><span class="sxs-lookup"><span data-stu-id="08aa4-647">445</span></span> |

<span data-ttu-id="08aa4-648">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span><span class="sxs-lookup"><span data-stu-id="08aa4-648">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="08aa4-649">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span><span class="sxs-lookup"><span data-stu-id="08aa4-649">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="08aa4-650">Service/load balancing rule name</span><span class="sxs-lookup"><span data-stu-id="08aa4-650">Service/load balancing rule name</span></span> | <span data-ttu-id="08aa4-651">Default port numbers</span><span class="sxs-lookup"><span data-stu-id="08aa4-651">Default port numbers</span></span> | <span data-ttu-id="08aa4-652">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span><span class="sxs-lookup"><span data-stu-id="08aa4-652">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa4-653">Enqueue Server / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="08aa4-653">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="08aa4-654">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-654">32<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-655">3201</span><span class="sxs-lookup"><span data-stu-id="08aa4-655">3201</span></span> |
| <span data-ttu-id="08aa4-656">Gateway Server / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="08aa4-656">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="08aa4-657">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-657">33<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-658">3301</span><span class="sxs-lookup"><span data-stu-id="08aa4-658">3301</span></span> |
| <span data-ttu-id="08aa4-659">Java Message Server / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="08aa4-659">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="08aa4-660">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-660">39<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-661">3901</span><span class="sxs-lookup"><span data-stu-id="08aa4-661">3901</span></span> |
| <span data-ttu-id="08aa4-662">Message Server HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="08aa4-662">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="08aa4-663">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="08aa4-663">81<*InstanceNumber*></span></span> |<span data-ttu-id="08aa4-664">8101</span><span class="sxs-lookup"><span data-stu-id="08aa4-664">8101</span></span> |
| <span data-ttu-id="08aa4-665">SAP Start Service SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="08aa4-665">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="08aa4-666">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="08aa4-666">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="08aa4-667">50113</span><span class="sxs-lookup"><span data-stu-id="08aa4-667">50113</span></span> |
| <span data-ttu-id="08aa4-668">SAP Start Service SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="08aa4-668">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="08aa4-669">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="08aa4-669">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="08aa4-670">50114</span><span class="sxs-lookup"><span data-stu-id="08aa4-670">50114</span></span> |
| <span data-ttu-id="08aa4-671">Enqueue Replication / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="08aa4-671">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="08aa4-672">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="08aa4-672">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="08aa4-673">50116</span><span class="sxs-lookup"><span data-stu-id="08aa4-673">50116</span></span> |
| <span data-ttu-id="08aa4-674">SAP Start Service ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="08aa4-674">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="08aa4-675">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="08aa4-675">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="08aa4-676">51113</span><span class="sxs-lookup"><span data-stu-id="08aa4-676">51113</span></span> |
| <span data-ttu-id="08aa4-677">SAP Start Service ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="08aa4-677">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="08aa4-678">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="08aa4-678">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="08aa4-679">51114</span><span class="sxs-lookup"><span data-stu-id="08aa4-679">51114</span></span> |
| <span data-ttu-id="08aa4-680">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="08aa4-680">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="08aa4-681">5985</span><span class="sxs-lookup"><span data-stu-id="08aa4-681">5985</span></span> |
| <span data-ttu-id="08aa4-682">File Share *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="08aa4-682">File Share *Lbrule445*</span></span> | |<span data-ttu-id="08aa4-683">445</span><span class="sxs-lookup"><span data-stu-id="08aa4-683">445</span></span> |

<span data-ttu-id="08aa4-684">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span><span class="sxs-lookup"><span data-stu-id="08aa4-684">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Figure 15: Default ASCS/SCS load balancing rules for the Azure internal load balancer][sap-ha-guide-figure-3004]

<span data-ttu-id="08aa4-686">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span><span class="sxs-lookup"><span data-stu-id="08aa4-686">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="08aa4-687">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-687">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> <span data-ttu-id="08aa4-688">Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span><span class="sxs-lookup"><span data-stu-id="08aa4-688">Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="08aa4-689">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span><span class="sxs-lookup"><span data-stu-id="08aa4-689">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="08aa4-690">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-690">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="08aa4-691">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span><span class="sxs-lookup"><span data-stu-id="08aa4-691">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="08aa4-692">Name</span><span class="sxs-lookup"><span data-stu-id="08aa4-692">Name</span></span>
  * <span data-ttu-id="08aa4-693">Port</span><span class="sxs-lookup"><span data-stu-id="08aa4-693">Port</span></span>
  * <span data-ttu-id="08aa4-694">Back-end port</span><span class="sxs-lookup"><span data-stu-id="08aa4-694">Back-end port</span></span>

  <span data-ttu-id="08aa4-695">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span><span class="sxs-lookup"><span data-stu-id="08aa4-695">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="08aa4-696">Here's an example of an update for port *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="08aa4-696">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figure 16: Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-figure-3005]

  <span data-ttu-id="08aa4-698">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span><span class="sxs-lookup"><span data-stu-id="08aa4-698">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> <span data-ttu-id="08aa4-699">Add Windows virtual machines to the domain</span><span class="sxs-lookup"><span data-stu-id="08aa4-699">Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="08aa4-700">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span><span class="sxs-lookup"><span data-stu-id="08aa4-700">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Figure 17: Add a virtual machine to a domain][sap-ha-guide-figure-3006]

<span data-ttu-id="08aa4-702">_**Figure 17:** Add a virtual machine to a domain_</span><span class="sxs-lookup"><span data-stu-id="08aa4-702">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> <span data-ttu-id="08aa4-703">Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-703">Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="08aa4-704">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span><span class="sxs-lookup"><span data-stu-id="08aa4-704">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="08aa4-705">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span><span class="sxs-lookup"><span data-stu-id="08aa4-705">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="08aa4-706">These connections usually remain established until the work process or the enqueue process restarts.</span><span class="sxs-lookup"><span data-stu-id="08aa4-706">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="08aa4-707">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span><span class="sxs-lookup"><span data-stu-id="08aa4-707">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="08aa4-708">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span><span class="sxs-lookup"><span data-stu-id="08aa4-708">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="08aa4-709">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span><span class="sxs-lookup"><span data-stu-id="08aa4-709">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="08aa4-710">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-710">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="08aa4-711">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span><span class="sxs-lookup"><span data-stu-id="08aa4-711">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="08aa4-712">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="08aa4-712">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="08aa4-713">Path</span><span class="sxs-lookup"><span data-stu-id="08aa4-713">Path</span></span> | <span data-ttu-id="08aa4-714">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="08aa4-714">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="08aa4-715">Variable name</span><span class="sxs-lookup"><span data-stu-id="08aa4-715">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="08aa4-716">Variable type</span><span class="sxs-lookup"><span data-stu-id="08aa4-716">Variable type</span></span> |<span data-ttu-id="08aa4-717">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="08aa4-717">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="08aa4-718">Value</span><span class="sxs-lookup"><span data-stu-id="08aa4-718">Value</span></span> |<span data-ttu-id="08aa4-719">120000</span><span class="sxs-lookup"><span data-stu-id="08aa4-719">120000</span></span> |
| <span data-ttu-id="08aa4-720">Link to documentation</span><span class="sxs-lookup"><span data-stu-id="08aa4-720">Link to documentation</span></span> |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="08aa4-721">_**Table 3:** Change the first TCP/IP parameter_</span><span class="sxs-lookup"><span data-stu-id="08aa4-721">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="08aa4-722">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="08aa4-722">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="08aa4-723">Path</span><span class="sxs-lookup"><span data-stu-id="08aa4-723">Path</span></span> | <span data-ttu-id="08aa4-724">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="08aa4-724">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="08aa4-725">Variable name</span><span class="sxs-lookup"><span data-stu-id="08aa4-725">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="08aa4-726">Variable type</span><span class="sxs-lookup"><span data-stu-id="08aa4-726">Variable type</span></span> |<span data-ttu-id="08aa4-727">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="08aa4-727">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="08aa4-728">Value</span><span class="sxs-lookup"><span data-stu-id="08aa4-728">Value</span></span> |<span data-ttu-id="08aa4-729">120000</span><span class="sxs-lookup"><span data-stu-id="08aa4-729">120000</span></span> |
| <span data-ttu-id="08aa4-730">Link to documentation</span><span class="sxs-lookup"><span data-stu-id="08aa4-730">Link to documentation</span></span> |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="08aa4-731">_**Table 4:** Change the second TCP/IP parameter_</span><span class="sxs-lookup"><span data-stu-id="08aa4-731">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="08aa4-732">**To apply the changes, restart both cluster nodes**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-732">**To apply the changes, restart both cluster nodes**.</span></span>

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> <span data-ttu-id="08aa4-733">Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-733">Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="08aa4-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span><span class="sxs-lookup"><span data-stu-id="08aa4-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="08aa4-735">Collecting the cluster nodes in a cluster configuration</span><span class="sxs-lookup"><span data-stu-id="08aa4-735">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="08aa4-736">Configuring a cluster file share witness</span><span class="sxs-lookup"><span data-stu-id="08aa4-736">Configuring a cluster file share witness</span></span>

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> <span data-ttu-id="08aa4-737">Collect the cluster nodes in a cluster configuration</span><span class="sxs-lookup"><span data-stu-id="08aa4-737">Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="08aa4-738">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-738">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="08aa4-739">Set up the failover cluster by using Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="08aa4-739">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="08aa4-740">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span><span class="sxs-lookup"><span data-stu-id="08aa4-740">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Figure 18: Add the server or virtual machine name of the first cluster node][sap-ha-guide-figure-3007]

  <span data-ttu-id="08aa4-742">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span><span class="sxs-lookup"><span data-stu-id="08aa4-742">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="08aa4-743">Enter the network name (virtual host name) of the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-743">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Figure 19: Enter the cluster name][sap-ha-guide-figure-3008]

  <span data-ttu-id="08aa4-745">_**Figure 19:** Enter the cluster name_</span><span class="sxs-lookup"><span data-stu-id="08aa4-745">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="08aa4-746">After you've created the cluster, run a cluster validation test.</span><span class="sxs-lookup"><span data-stu-id="08aa4-746">After you've created the cluster, run a cluster validation test.</span></span>

  ![Figure 20: Run the cluster validation check][sap-ha-guide-figure-3009]

  <span data-ttu-id="08aa4-748">_**Figure 20:** Run the cluster validation check_</span><span class="sxs-lookup"><span data-stu-id="08aa4-748">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="08aa4-749">You can ignore any warnings about disks at this point in the process.</span><span class="sxs-lookup"><span data-stu-id="08aa4-749">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="08aa4-750">You'll add a file share witness and the SIOS shared disks later.</span><span class="sxs-lookup"><span data-stu-id="08aa4-750">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="08aa4-751">At this stage, you don't need to worry about having a quorum.</span><span class="sxs-lookup"><span data-stu-id="08aa4-751">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Figure 21: No quorum disk is found][sap-ha-guide-figure-3010]

  <span data-ttu-id="08aa4-753">_**Figure 21:** No quorum disk is found_</span><span class="sxs-lookup"><span data-stu-id="08aa4-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figure 22: Core cluster resource needs a new IP address][sap-ha-guide-figure-3011]

  <span data-ttu-id="08aa4-755">_**Figure 22:** Core cluster resource needs a new IP address_</span><span class="sxs-lookup"><span data-stu-id="08aa4-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="08aa4-756">Change the IP address of the core cluster service.</span><span class="sxs-lookup"><span data-stu-id="08aa4-756">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="08aa4-757">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-757">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="08aa4-758">Do this on the **Properties** page of the core cluster service's IP resource.</span><span class="sxs-lookup"><span data-stu-id="08aa4-758">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="08aa4-759">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-759">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figure 23: In the Properties dialog box, change the IP address][sap-ha-guide-figure-3012]

  <span data-ttu-id="08aa4-761">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span><span class="sxs-lookup"><span data-stu-id="08aa4-761">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Figure 24: Assign the IP address that is reserved for the cluster][sap-ha-guide-figure-3013]

  <span data-ttu-id="08aa4-763">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span><span class="sxs-lookup"><span data-stu-id="08aa4-763">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="08aa4-764">Bring the cluster virtual host name online.</span><span class="sxs-lookup"><span data-stu-id="08aa4-764">Bring the cluster virtual host name online.</span></span>

  ![Figure 25: Cluster core service is up and running, and with the correct IP address][sap-ha-guide-figure-3014]

  <span data-ttu-id="08aa4-766">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span><span class="sxs-lookup"><span data-stu-id="08aa4-766">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="08aa4-767">Add the second cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-767">Add the second cluster node.</span></span>

  <span data-ttu-id="08aa4-768">Now that the core cluster service is up and running, you can add the second cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-768">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Figure 26: Add the second cluster node][sap-ha-guide-figure-3015]

  <span data-ttu-id="08aa4-770">_**Figure 26:** Add the second cluster node_</span><span class="sxs-lookup"><span data-stu-id="08aa4-770">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="08aa4-771">Enter a name for the second cluster node host.</span><span class="sxs-lookup"><span data-stu-id="08aa4-771">Enter a name for the second cluster node host.</span></span>

  ![Figure 27: Enter the second cluster node host name][sap-ha-guide-figure-3016]

  <span data-ttu-id="08aa4-773">_**Figure 27:** Enter the second cluster node host name_</span><span class="sxs-lookup"><span data-stu-id="08aa4-773">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="08aa4-774">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span><span class="sxs-lookup"><span data-stu-id="08aa4-774">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figure 28: Do not select the check box][sap-ha-guide-figure-3017]

  <span data-ttu-id="08aa4-776">_**Figure 28:** Do **not** select the check box_</span><span class="sxs-lookup"><span data-stu-id="08aa4-776">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="08aa4-777">You can ignore warnings about quorum and disks.</span><span class="sxs-lookup"><span data-stu-id="08aa4-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="08aa4-778">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="08aa4-778">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figure 29: Ignore warnings about the disk quorum][sap-ha-guide-figure-3018]

  <span data-ttu-id="08aa4-780">_**Figure 29:** Ignore warnings about the disk quorum_</span><span class="sxs-lookup"><span data-stu-id="08aa4-780">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> <span data-ttu-id="08aa4-781">Configure a cluster file share witness</span><span class="sxs-lookup"><span data-stu-id="08aa4-781">Configure a cluster file share witness</span></span>

<span data-ttu-id="08aa4-782">Configuring a cluster file share witness involves these tasks:</span><span class="sxs-lookup"><span data-stu-id="08aa4-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="08aa4-783">Creating a file share</span><span class="sxs-lookup"><span data-stu-id="08aa4-783">Creating a file share</span></span>
- <span data-ttu-id="08aa4-784">Setting the file share witness quorum in Failover Cluster Manager</span><span class="sxs-lookup"><span data-stu-id="08aa4-784">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> <span data-ttu-id="08aa4-785">Create a file share</span><span class="sxs-lookup"><span data-stu-id="08aa4-785">Create a file share</span></span>

1.  <span data-ttu-id="08aa4-786">Select a file share witness instead of a quorum disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="08aa4-787">SIOS DataKeeper supports this option.</span><span class="sxs-lookup"><span data-stu-id="08aa4-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="08aa4-788">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-788">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="08aa4-789">The file share witness is called **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-789">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="08aa4-790">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span><span class="sxs-lookup"><span data-stu-id="08aa4-790">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08aa4-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span><span class="sxs-lookup"><span data-stu-id="08aa4-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="08aa4-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="08aa4-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="08aa4-793">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-793">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="08aa4-794">The quorum drive needs at least 1,024 MB of free space.</span><span class="sxs-lookup"><span data-stu-id="08aa4-794">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="08aa4-795">We recommend 2,048 MB of free space for the quorum drive.</span><span class="sxs-lookup"><span data-stu-id="08aa4-795">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="08aa4-796">Add the cluster name object.</span><span class="sxs-lookup"><span data-stu-id="08aa4-796">Add the cluster name object.</span></span>

  ![Figure 30: Assign the permissions on the share for the cluster name object][sap-ha-guide-figure-3019]

  <span data-ttu-id="08aa4-798">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span><span class="sxs-lookup"><span data-stu-id="08aa4-798">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="08aa4-799">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="08aa4-799">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="08aa4-800">To add the cluster name object to the list, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-800">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="08aa4-801">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span><span class="sxs-lookup"><span data-stu-id="08aa4-801">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Figure 31: Change the Object Types to include computers][sap-ha-guide-figure-3020]

  <span data-ttu-id="08aa4-803">_**Figure 31:** Change the Object Types to include computers_</span><span class="sxs-lookup"><span data-stu-id="08aa4-803">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Figure 32: Select the Computers check box][sap-ha-guide-figure-3021]

  <span data-ttu-id="08aa4-805">_**Figure 32:** Select the **Computers** check box_</span><span class="sxs-lookup"><span data-stu-id="08aa4-805">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="08aa4-806">Enter the cluster name object as shown in Figure 31.</span><span class="sxs-lookup"><span data-stu-id="08aa4-806">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="08aa4-807">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span><span class="sxs-lookup"><span data-stu-id="08aa4-807">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="08aa4-808">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span><span class="sxs-lookup"><span data-stu-id="08aa4-808">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Figure 33: Set the security attributes for the cluster name object on the file share quorum][sap-ha-guide-figure-3022]

  <span data-ttu-id="08aa4-810">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span><span class="sxs-lookup"><span data-stu-id="08aa4-810">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> <span data-ttu-id="08aa4-811">Set the file share witness quorum in Failover Cluster Manager</span><span class="sxs-lookup"><span data-stu-id="08aa4-811">Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="08aa4-812">Open the Configure Quorum Setting Wizard.</span><span class="sxs-lookup"><span data-stu-id="08aa4-812">Open the Configure Quorum Setting Wizard.</span></span>

  ![Figure 34: Start the Configure Cluster Quorum Setting Wizard][sap-ha-guide-figure-3023]

  <span data-ttu-id="08aa4-814">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span><span class="sxs-lookup"><span data-stu-id="08aa4-814">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="08aa4-815">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-815">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Figure 35: Quorum configurations you can choose from][sap-ha-guide-figure-3024]

  <span data-ttu-id="08aa4-817">_**Figure 35:** Quorum configurations you can choose from_</span><span class="sxs-lookup"><span data-stu-id="08aa4-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="08aa4-818">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-818">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figure 36: Select the file share witness][sap-ha-guide-figure-3025]

  <span data-ttu-id="08aa4-820">_**Figure 36:** Select the file share witness_</span><span class="sxs-lookup"><span data-stu-id="08aa4-820">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="08aa4-821">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span><span class="sxs-lookup"><span data-stu-id="08aa4-821">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="08aa4-822">To see a list of the changes you can make, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-822">To see a list of the changes you can make, select **Next**.</span></span>

  ![Figure 37: Define the file share location for the witness share][sap-ha-guide-figure-3026]

  <span data-ttu-id="08aa4-824">_**Figure 37:** Define the file share location for the witness share_</span><span class="sxs-lookup"><span data-stu-id="08aa4-824">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="08aa4-825">Select the changes you want, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-825">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="08aa4-826">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span><span class="sxs-lookup"><span data-stu-id="08aa4-826">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![Figure 38: Confirmation that you've reconfigured the cluster][sap-ha-guide-figure-3027]

  <span data-ttu-id="08aa4-828">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span><span class="sxs-lookup"><span data-stu-id="08aa4-828">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="08aa4-829">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-829">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="08aa4-830">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span><span class="sxs-lookup"><span data-stu-id="08aa4-830">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="08aa4-831">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span><span class="sxs-lookup"><span data-stu-id="08aa4-831">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="08aa4-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="08aa4-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="08aa4-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="08aa4-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="08aa4-834">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span><span class="sxs-lookup"><span data-stu-id="08aa4-834">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="08aa4-835">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-835">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> <span data-ttu-id="08aa4-836">Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span><span class="sxs-lookup"><span data-stu-id="08aa4-836">Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="08aa4-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="08aa4-838">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span><span class="sxs-lookup"><span data-stu-id="08aa4-838">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="08aa4-839">You cannot create the shared disk resources you need in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-839">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="08aa4-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span><span class="sxs-lookup"><span data-stu-id="08aa4-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="08aa4-841">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span><span class="sxs-lookup"><span data-stu-id="08aa4-841">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="08aa4-842">Adding the .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="08aa4-842">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="08aa4-843">Installing SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="08aa4-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="08aa4-844">Setting up SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="08aa4-844">Setting up SIOS DataKeeper</span></span>

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> <span data-ttu-id="08aa4-845">Add the .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="08aa4-845">Add the .NET Framework 3.5</span></span>
<span data-ttu-id="08aa4-846">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="08aa4-846">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="08aa4-847">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-847">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="08aa4-848">There are two ways to add the .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="08aa4-848">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="08aa4-849">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span><span class="sxs-lookup"><span data-stu-id="08aa4-849">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figure 39: Install the .NET Framework 3.5 by using the Add Roles and Features Wizard][sap-ha-guide-figure-3028]

  <span data-ttu-id="08aa4-851">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span><span class="sxs-lookup"><span data-stu-id="08aa4-851">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Figure 40: Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard][sap-ha-guide-figure-3029]

  <span data-ttu-id="08aa4-853">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span><span class="sxs-lookup"><span data-stu-id="08aa4-853">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="08aa4-854">Use the command-line tool dism.exe.</span><span class="sxs-lookup"><span data-stu-id="08aa4-854">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="08aa4-855">For this type of installation, you need to access the SxS directory on the Windows installation media.</span><span class="sxs-lookup"><span data-stu-id="08aa4-855">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="08aa4-856">At an elevated command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="08aa4-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> <span data-ttu-id="08aa4-857">Install SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="08aa4-857">Install SIOS DataKeeper</span></span>

<span data-ttu-id="08aa4-858">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="08aa4-858">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="08aa4-859">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span><span class="sxs-lookup"><span data-stu-id="08aa4-859">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="08aa4-860">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-860">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-861">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-861">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="08aa4-862">To install SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="08aa4-862">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="08aa4-863">Install the SIOS software on both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-863">Install the SIOS software on both cluster nodes.</span></span>

  ![SIOS installer][sap-ha-guide-figure-3030]

  ![Figure 41: First page of the SIOS DataKeeper installation][sap-ha-guide-figure-3031]

  <span data-ttu-id="08aa4-866">_**Figure 41:** First page of the SIOS DataKeeper installation_</span><span class="sxs-lookup"><span data-stu-id="08aa4-866">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="08aa4-867">In the dialog box shown in Figure 42, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-867">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figure 42: DataKeeper informs you that a service will be disabled][sap-ha-guide-figure-3032]

  <span data-ttu-id="08aa4-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span><span class="sxs-lookup"><span data-stu-id="08aa4-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="08aa4-870">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-870">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figure 43: User selection for SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="08aa4-872">_**Figure 43:** User selection for SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="08aa4-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="08aa4-873">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="08aa4-873">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figure 44: Enter the domain user name and password for the SIOS DataKeeper installation][sap-ha-guide-figure-3034]

  <span data-ttu-id="08aa4-875">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span><span class="sxs-lookup"><span data-stu-id="08aa4-875">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="08aa4-876">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span><span class="sxs-lookup"><span data-stu-id="08aa4-876">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figure 45: Enter your SIOS DataKeeper license key][sap-ha-guide-figure-3035]

  <span data-ttu-id="08aa4-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span><span class="sxs-lookup"><span data-stu-id="08aa4-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="08aa4-879">When prompted, restart the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-879">When prompted, restart the virtual machine.</span></span>

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> <span data-ttu-id="08aa4-880">Set up SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="08aa4-880">Set up SIOS DataKeeper</span></span>

<span data-ttu-id="08aa4-881">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span><span class="sxs-lookup"><span data-stu-id="08aa4-881">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="08aa4-882">The goal of the configuration is to have synchronous data replication between the additional VHDs attached to each of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-882">The goal of the configuration is to have synchronous data replication between the additional VHDs attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="08aa4-883">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-883">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="08aa4-884">(In Figure 46, this option is circled in red.)</span><span class="sxs-lookup"><span data-stu-id="08aa4-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figure 46: SIOS DataKeeper Management and Configuration tool][sap-ha-guide-figure-3036]

  <span data-ttu-id="08aa4-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span><span class="sxs-lookup"><span data-stu-id="08aa4-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="08aa4-887">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-887">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Figure 47: Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node][sap-ha-guide-figure-3037]

  <span data-ttu-id="08aa4-889">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span><span class="sxs-lookup"><span data-stu-id="08aa4-889">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="08aa4-890">Create the replication job between the two nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-890">Create the replication job between the two nodes.</span></span>

  ![Figure 48: Create a replication job][sap-ha-guide-figure-3038]

  <span data-ttu-id="08aa4-892">_**Figure 48:** Create a replication job_</span><span class="sxs-lookup"><span data-stu-id="08aa4-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="08aa4-893">A wizard guides you through the process of creating a replication job.</span><span class="sxs-lookup"><span data-stu-id="08aa4-893">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="08aa4-894">Define the name, TCP/IP address, and disk volume of the source node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-894">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Figure 49: Define the name of the replication job][sap-ha-guide-figure-3039]

  <span data-ttu-id="08aa4-896">_**Figure 49:** Define the name of the replication job_</span><span class="sxs-lookup"><span data-stu-id="08aa4-896">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Figure 50: Define the base data for the node, which should be the current source node][sap-ha-guide-figure-3040]

  <span data-ttu-id="08aa4-898">_**Figure 50:** Define the base data for the node, which should be the current source node_</span><span class="sxs-lookup"><span data-stu-id="08aa4-898">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="08aa4-899">Define the name, TCP/IP address, and disk volume of the target node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-899">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Figure 51: Define the base data for the node, which should be the current target node][sap-ha-guide-figure-3041]

  <span data-ttu-id="08aa4-901">_**Figure 51:** Define the base data for the node, which should be the current target node_</span><span class="sxs-lookup"><span data-stu-id="08aa4-901">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="08aa4-902">Define the compression algorithms.</span><span class="sxs-lookup"><span data-stu-id="08aa4-902">Define the compression algorithms.</span></span> <span data-ttu-id="08aa4-903">In our example, we recommend that you compress the replication stream.</span><span class="sxs-lookup"><span data-stu-id="08aa4-903">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="08aa4-904">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span><span class="sxs-lookup"><span data-stu-id="08aa4-904">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="08aa4-905">Note that compression uses the CPU and RAM resources of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-905">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="08aa4-906">As the compression rate increases, so does the volume of CPU resources used.</span><span class="sxs-lookup"><span data-stu-id="08aa4-906">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="08aa4-907">You also can adjust this setting later.</span><span class="sxs-lookup"><span data-stu-id="08aa4-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="08aa4-908">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span><span class="sxs-lookup"><span data-stu-id="08aa4-908">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="08aa4-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span><span class="sxs-lookup"><span data-stu-id="08aa4-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figure 52: Define replication details][sap-ha-guide-figure-3042]

  <span data-ttu-id="08aa4-911">_**Figure 52:** Define replication details_</span><span class="sxs-lookup"><span data-stu-id="08aa4-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="08aa4-912">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span><span class="sxs-lookup"><span data-stu-id="08aa4-912">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="08aa4-913">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span><span class="sxs-lookup"><span data-stu-id="08aa4-913">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figure 53: Select Yes to set the replicated volume as a cluster volume][sap-ha-guide-figure-3043]

  <span data-ttu-id="08aa4-915">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span><span class="sxs-lookup"><span data-stu-id="08aa4-915">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="08aa4-916">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span><span class="sxs-lookup"><span data-stu-id="08aa4-916">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Figure 54: DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active][sap-ha-guide-figure-3044]

  <span data-ttu-id="08aa4-918">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span><span class="sxs-lookup"><span data-stu-id="08aa4-918">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="08aa4-919">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span><span class="sxs-lookup"><span data-stu-id="08aa4-919">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figure 55: Failover Cluster Manager shows the disk that DataKeeper replicated][sap-ha-guide-figure-3045]

  <span data-ttu-id="08aa4-921">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span><span class="sxs-lookup"><span data-stu-id="08aa4-921">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> <span data-ttu-id="08aa4-922">Install the SAP NetWeaver system</span><span class="sxs-lookup"><span data-stu-id="08aa4-922">Install the SAP NetWeaver system</span></span>

<span data-ttu-id="08aa4-923">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span><span class="sxs-lookup"><span data-stu-id="08aa4-923">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="08aa4-924">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-924">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="08aa4-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span><span class="sxs-lookup"><span data-stu-id="08aa4-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="08aa4-926">In the scenario we use in this article, we didn't add more protection to the DBMS.</span><span class="sxs-lookup"><span data-stu-id="08aa4-926">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="08aa4-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span><span class="sxs-lookup"><span data-stu-id="08aa4-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-928">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span><span class="sxs-lookup"><span data-stu-id="08aa4-928">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="08aa4-929">The most significant difference is that an SAP ABAP system has one ASCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-929">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="08aa4-930">The SAP Java system has one SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-930">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="08aa4-931">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span><span class="sxs-lookup"><span data-stu-id="08aa4-931">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="08aa4-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span><span class="sxs-lookup"><span data-stu-id="08aa4-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="08aa4-933">You can assume that all other parts are the same.</span><span class="sxs-lookup"><span data-stu-id="08aa4-933">You can assume that all other parts are the same.</span></span>  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> <span data-ttu-id="08aa4-934">Install SAP with a high-availability ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-934">Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08aa4-935">Be sure not to place your page file on DataKeeper mirrored volumes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-935">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="08aa4-936">DataKeeper does not support mirrored volumes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="08aa4-937">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span><span class="sxs-lookup"><span data-stu-id="08aa4-937">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="08aa4-938">If it's not already there, move the Windows page file to drive D of your Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="08aa4-938">If it's not already there, move the Windows page file to drive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="08aa4-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span><span class="sxs-lookup"><span data-stu-id="08aa4-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="08aa4-940">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-940">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="08aa4-941">Installing the SAP first cluster node</span><span class="sxs-lookup"><span data-stu-id="08aa4-941">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="08aa4-942">Modifying the SAP profile of the ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-942">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="08aa4-943">Adding a probe port</span><span class="sxs-lookup"><span data-stu-id="08aa4-943">Adding a probe port</span></span>
- <span data-ttu-id="08aa4-944">Opening the Windows firewall probe port</span><span class="sxs-lookup"><span data-stu-id="08aa4-944">Opening the Windows firewall probe port</span></span>

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> <span data-ttu-id="08aa4-945">Create a virtual host name for the clustered SAP ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-945">Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="08aa4-946">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-946">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="08aa4-947">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="08aa4-947">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="08aa4-948">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="08aa4-948">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figure 56: Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address][sap-ha-guide-figure-3046]

  <span data-ttu-id="08aa4-950">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span><span class="sxs-lookup"><span data-stu-id="08aa4-950">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="08aa4-951">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-951">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figure 57: New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration][sap-ha-guide-figure-3047]

  <span data-ttu-id="08aa4-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span><span class="sxs-lookup"><span data-stu-id="08aa4-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> <span data-ttu-id="08aa4-954">Install the SAP first cluster node</span><span class="sxs-lookup"><span data-stu-id="08aa4-954">Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="08aa4-955">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span><span class="sxs-lookup"><span data-stu-id="08aa4-955">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="08aa4-956">To keep the default ports for the Azure internal load balancer, select:</span><span class="sxs-lookup"><span data-stu-id="08aa4-956">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="08aa4-957">**ABAP system**: **ASCS** instance number **00**</span><span class="sxs-lookup"><span data-stu-id="08aa4-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="08aa4-958">**Java system**: **SCS** instance number **01**</span><span class="sxs-lookup"><span data-stu-id="08aa4-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="08aa4-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span><span class="sxs-lookup"><span data-stu-id="08aa4-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="08aa4-960">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="08aa4-960">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="08aa4-961">The next few tasks aren't described in the standard SAP installation documentation.</span><span class="sxs-lookup"><span data-stu-id="08aa4-961">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-962">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span><span class="sxs-lookup"><span data-stu-id="08aa4-962">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> <span data-ttu-id="08aa4-963">Modify the SAP profile of the ASCS/SCS instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-963">Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="08aa4-964">You need to add a new profile parameter.</span><span class="sxs-lookup"><span data-stu-id="08aa4-964">You need to add a new profile parameter.</span></span> <span data-ttu-id="08aa4-965">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span><span class="sxs-lookup"><span data-stu-id="08aa4-965">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="08aa4-966">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="08aa4-966">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="08aa4-967">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span><span class="sxs-lookup"><span data-stu-id="08aa4-967">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="08aa4-968">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span><span class="sxs-lookup"><span data-stu-id="08aa4-968">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="08aa4-969">To modify the SAP profile of the ASCS/SCS instance:</span><span class="sxs-lookup"><span data-stu-id="08aa4-969">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="08aa4-970">Add this profile parameter to the SAP ASCS/SCS instance profile:</span><span class="sxs-lookup"><span data-stu-id="08aa4-970">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="08aa4-971">In our example, the path is:</span><span class="sxs-lookup"><span data-stu-id="08aa4-971">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="08aa4-972">For example, to the SAP SCS instance profile and corresponding path:</span><span class="sxs-lookup"><span data-stu-id="08aa4-972">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="08aa4-973">To apply the changes, restart the SAP ASCS /SCS instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-973">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> <span data-ttu-id="08aa4-974">Add a probe port</span><span class="sxs-lookup"><span data-stu-id="08aa4-974">Add a probe port</span></span>

<span data-ttu-id="08aa4-975">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa4-975">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="08aa4-976">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span><span class="sxs-lookup"><span data-stu-id="08aa4-976">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="08aa4-977">However, this won't work in some cluster configurations because only one instance is active.</span><span class="sxs-lookup"><span data-stu-id="08aa4-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="08aa4-978">The other instance is passive and can’t accept any of the workload.</span><span class="sxs-lookup"><span data-stu-id="08aa4-978">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="08aa4-979">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-979">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="08aa4-980">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span><span class="sxs-lookup"><span data-stu-id="08aa4-980">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="08aa4-981">To add a probe port:</span><span class="sxs-lookup"><span data-stu-id="08aa4-981">To add a probe port:</span></span>

1.  <span data-ttu-id="08aa4-982">Check the current **ProbePort** setting by running the following PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="08aa4-982">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="08aa4-983">Execute it from within one of the virtual machines in the cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="08aa4-983">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="08aa4-984">Define a probe port.</span><span class="sxs-lookup"><span data-stu-id="08aa4-984">Define a probe port.</span></span> <span data-ttu-id="08aa4-985">The default probe port number is **0**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-985">The default probe port number is **0**.</span></span> <span data-ttu-id="08aa4-986">In our example, we use probe port **62000**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-986">In our example, we use probe port **62000**.</span></span>

  ![Figure 58: The cluster configuration probe port is 0 by default][sap-ha-guide-figure-3048]

  <span data-ttu-id="08aa4-988">_**Figure 58:** The default cluster configuration probe port is 0_</span><span class="sxs-lookup"><span data-stu-id="08aa4-988">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="08aa4-989">The port number is defined in SAP Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="08aa4-989">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="08aa4-990">You can assign the port number in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08aa4-990">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="08aa4-991">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="08aa4-991">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="08aa4-992">Update the PowerShell variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-992">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="08aa4-993">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-993">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="08aa4-994">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span><span class="sxs-lookup"><span data-stu-id="08aa4-994">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figure 59: Probe the cluster port after you set the new value][sap-ha-guide-figure-3049]

  <span data-ttu-id="08aa4-996">_**Figure 59:** Probe the cluster port after you set the new value_</span><span class="sxs-lookup"><span data-stu-id="08aa4-996">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> <span data-ttu-id="08aa4-997">Open the Windows firewall probe port</span><span class="sxs-lookup"><span data-stu-id="08aa4-997">Open the Windows firewall probe port</span></span>

<span data-ttu-id="08aa4-998">You need to open a Windows firewall probe port on both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-998">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="08aa4-999">Use the following script to open a Windows firewall probe port.</span><span class="sxs-lookup"><span data-stu-id="08aa4-999">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="08aa4-1000">Update the PowerShell variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1000">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="08aa4-1001">The **ProbePort** is set to **62000**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1001">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="08aa4-1002">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1002">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> <span data-ttu-id="08aa4-1003">Install the database instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-1003">Install the database instance</span></span>

<span data-ttu-id="08aa4-1004">To install the database instance, follow the process described in the SAP installation documentation.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1004">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> <span data-ttu-id="08aa4-1005">Install the second cluster node</span><span class="sxs-lookup"><span data-stu-id="08aa4-1005">Install the second cluster node</span></span>

<span data-ttu-id="08aa4-1006">To install the second cluster, follow the steps in the SAP installation guide.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1006">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> <span data-ttu-id="08aa4-1007">Change the start type of the SAP ERS Windows service instance</span><span class="sxs-lookup"><span data-stu-id="08aa4-1007">Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="08aa4-1008">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1008">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figure 60: Change the service type for the SAP ERS instance to delayed automatic][sap-ha-guide-figure-3050]

<span data-ttu-id="08aa4-1010">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span><span class="sxs-lookup"><span data-stu-id="08aa4-1010">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> <span data-ttu-id="08aa4-1011">Install the SAP Primary Application Server</span><span class="sxs-lookup"><span data-stu-id="08aa4-1011">Install the SAP Primary Application Server</span></span>

<span data-ttu-id="08aa4-1012">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1012">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="08aa4-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> <span data-ttu-id="08aa4-1014">Install the SAP Additional Application Server</span><span class="sxs-lookup"><span data-stu-id="08aa4-1014">Install the SAP Additional Application Server</span></span>

<span data-ttu-id="08aa4-1015">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1015">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="08aa4-1016">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1016">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="08aa4-1017">This finishes the installation of a high-availability SAP NetWeaver system.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1017">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="08aa4-1018">Next, proceed with failover testing.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1018">Next, proceed with failover testing.</span></span>
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> <span data-ttu-id="08aa4-1019">Test the SAP ASCS/SCS instance failover and SIOS replication</span><span class="sxs-lookup"><span data-stu-id="08aa4-1019">Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="08aa4-1020">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1020">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> <span data-ttu-id="08aa4-1021">SAP ASCS/SCS instance is running on cluster node A</span><span class="sxs-lookup"><span data-stu-id="08aa4-1021">SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="08aa4-1022">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1022">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="08aa4-1023">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1023">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Figure 61: Failover Cluster Manager: The SAP <SID> cluster group is running on cluster node A][sap-ha-guide-figure-5000]

<span data-ttu-id="08aa4-1025">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span><span class="sxs-lookup"><span data-stu-id="08aa4-1025">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="08aa4-1026">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1026">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figure 62: In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B][sap-ha-guide-figure-5001]

<span data-ttu-id="08aa4-1028">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span><span class="sxs-lookup"><span data-stu-id="08aa4-1028">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> <span data-ttu-id="08aa4-1029">Failover from node A to node B</span><span class="sxs-lookup"><span data-stu-id="08aa4-1029">Failover from node A to node B</span></span>

1.  <span data-ttu-id="08aa4-1030">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span><span class="sxs-lookup"><span data-stu-id="08aa4-1030">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="08aa4-1031">Use Failover Cluster Manager</span><span class="sxs-lookup"><span data-stu-id="08aa4-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="08aa4-1032">Use Failover Cluster PowerShell</span><span class="sxs-lookup"><span data-stu-id="08aa4-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="08aa4-1033">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span><span class="sxs-lookup"><span data-stu-id="08aa4-1033">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="08aa4-1034">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span><span class="sxs-lookup"><span data-stu-id="08aa4-1034">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="08aa4-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span><span class="sxs-lookup"><span data-stu-id="08aa4-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="08aa4-1036">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1036">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figure 63: In Failover Cluster Manager, the SAP <SID> cluster group is running on cluster node B][sap-ha-guide-figure-5002]

  <span data-ttu-id="08aa4-1038">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span><span class="sxs-lookup"><span data-stu-id="08aa4-1038">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="08aa4-1039">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="08aa4-1039">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figure 64: SIOS DataKeeper replicates the local volume from cluster node B to cluster node A][sap-ha-guide-figure-5003]

  <span data-ttu-id="08aa4-1041">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span><span class="sxs-lookup"><span data-stu-id="08aa4-1041">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>















































































































