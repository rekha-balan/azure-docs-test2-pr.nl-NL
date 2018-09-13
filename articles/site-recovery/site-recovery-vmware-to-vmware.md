---
title: Replicate VMware VMs or physical servers to another site (classic Azure portal) | Microsoft Docs
description: Use this article to replicate VMware VMs or Windows/Linux physical servers to a secondary site with Azure Site Recovery.
services: site-recovery
documentationcenter: ''
author: nsoneji
manager: jwhit
editor: ''
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: nisoneji
ms.openlocfilehash: 46872ed8a974bbd25df154aceb305933df1b92c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563721"
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-to-a-secondary-site-in-the-classic-azure-portal"></a>Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal

## <a name="overview"></a>Overview
InMage Scout in Azure Site Recovery provides real-time replication between on-premises VMware sites. InMage Scout is included in Azure Site Recovery service subscriptions.

## <a name="prerequisites"></a>Prerequisites
**Azure account**: You'll need a [Microsoft Azure](https://azure.microsoft.com/) account. You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/). [Learn more](https://azure.microsoft.com/pricing/details/site-recovery/) about Site Recovery pricing.

## <a name="step-1-create-a-vault"></a>Step 1: Create a vault
1. Sign in to the [Azure portal](https://portal.azure.com).
2. Click New > Management > Backup and Site Recovery (OMS). Alternatively, you can click Browse > Recovery Services Vault > Add.
3. In **Name** specify a friendly name to identify the vault. If you have more than one subscription, select one of them.
4. In **Resource group** Create a new resource group or select an existing one. Specify an Azure region to complete required fields.
5. In **Location**, select the geographic region for the vault. To check supported regions, see [Azure Site Recovery Pricing](https://azure.microsoft.com/pricing/details/site-recovery/).
6. If you want to quickly access the vault from the Dashboard click Pin to dashboard and then click Create.
7. The new vault will appear on the Dashboard > All resources, and on the main Recovery Services vaults blade.

## <a name="step-2-configure-the-vault-and-download-inmage-scout-components"></a>Step 2: Configure the vault and download InMage Scout components
1. In the Recovery Services vaults blade select your vault and click Settings.
2. In **Settings** > **Getting Started** click **Site Recovery** > Step 1: **Prepare Infrastructure** > **Protection goal**.
3. In **Protection goal** select To recovery site, and select Yes, with VMware vSphere Hypervisor. Then click OK.
4. In **Scout setup**, click download to download InMage Scout 8.0.1 GA software and registration key. The setup files for all of the required components are in the downloaded .zip file.

## <a name="step-3-install-component-updates"></a>Step 3: Install component updates
Read about the latest [updates](#updates). You'll install the update files on servers in the following order:

1. RX server if there is one
2. Configuration servers
3. Process servers
4. Master target servers
5. vContinuum servers
6. Source server (both Windows and Linux Server)

Install the updates as follows:

1. Download the [update](https://aka.ms/asr-scout-update4) .zip file. This .zip file contains the following files:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.4.0_GA_Update_4_9035261_27Sep16.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.4.0_GA_Update_4_8921562_16Sep16.exe
   * UA update4 bits for RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Extract the .zip files.<br>
3. **For the RX server**: Copy **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** to the RX server and extract it. In the extracted folder, run **/Install**.<br>
4. **For the configuration server/process server**: Copy **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** to the configuration server and process server. Double-click to run it.<br>
5. **For the Windows master target server**: To update the unified agent, copy **UA_Windows_8.0.4.0_GA_Update_4_9035261_27Sep16.exe** to the master target server. Double-click it to run it. Note that the unified agent is also applicable to the source server. You should install it on the source server as well, as mentioned later in this list.<br>
6. **For the vContinuum server**:  Copy **vCon_Windows_8.0.4.0_GA_Update_4_8921562_16Sep16.exe** to the vContinuum server.  Make sure that you've closed the vContinuum wizard. Double-click on the file to run it.<br>
7. **For the Linux master target server**: To update the unified agent, copy **UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** to the master target server and extract it. In the extracted folder, run **/Install**.<br>
8. **For the Windows source server**: To update the unified agent, copy **UA_Windows_8.0.4.0_GA_Update_4_9035261_27Sep16.exe** to the source server. Double-click it to run it.<br>
9. **For the Linux source server**: To update the unified agent, copy corresponding  version of UA file to the Linux server and extract it. In the extracted folder, run **/Install**.  Example: For RHEL 6.7 64 bit server,  copy **UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz**  to the server and extract it. In the extracted folder, run **/Install**.

## <a name="step-4-set-up-replication"></a>Step 4: Set up replication
1. Set up replication between the source and target VMware sites.
2. For guidance, use the InMage Scout documentation that's downloaded with the product. Alternatively, you can access the documentation as follows:

   * [Release notes](https://aka.ms/asr-scout-release-notes)
   * [Compatibility matrix](https://aka.ms/asr-scout-cm)
   * [User guide](https://aka.ms/asr-scout-user-guide)
   * [RX user guide](https://aka.ms/asr-scout-rx-user-guide)
   * [Quick installation guide](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Updates
### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Update 4
Scout Update 4 is a cumulative update. It has all the fixes of update1 till update3 and following new bug fixes and enhancements.

**New platform support**

* Support has been added for vCenter/vSphere 6.0, 6.1 and 6.2
* Support has been added for following Linux operating systems
  * Red Hat Enterprise Linux (RHEL)7.0, 7.1 and 7.2
  * CentOS 7.0, 7.1 and 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64 bit  **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** is packaged with base Scout GA package **InMage_Scout_Standard_8.0.1 GA.zip**. Download Scout GA package from portal as mentioned in [step 1](#step-1-create-a-vault).
>
>

**Bug fixes and enhancements**

* Improved shutdown handling for following Linux OSes and clones to prevent unwanted re-sync issues.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* For Linux, complete folder access permissions in unified agent installation directory are now restricted only to the local user.
* On Windows timing out issue while issuing  common distributed consistency book mark on heavily loaded distributed applications like SQL and Share Point clusters.
* Added log related fix in CX base installer.
* VMware vCLI 6.0 download link is added to Windows Master Target base installer.
* Added more checks and logs for network configurations changes during failover and DR drills.
* Sometime retention information is not reported to the CX.  
* For physical cluster, volume Re-size operation through vContinuum wizard is failing when source volume shrink happened.
* Cluster protection failed with error "Failed to find the disk signature" when cluster disk is PRDM disk.
* cxps transport server crash because of out-of-range exception.
* Server name and IP columns are now resizable in push install page of vContinuum wizard.
* RX API Enhancements
  * Provides Five latest available common consistency points (Only Guaranteed tags).
  * Provides capacity and free space details for all the protected devices.
  * Provides Scout driver state on source server.

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** base package now has updated CX base installer **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe**  and Windows Master Target  base installer **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. For all new installation use new CX and Windows Master Target GA bits.
> * Update 4 can be directly applied on 8.0.1 GA.
> * The configuration server and RX updates can’t be rolled back after they're applied on the system.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 Update 3
Update 3 includes the following bug fixes and enhancements:

* The configuration server and RX fail to register to the Site Recovery vault when they're behind the proxy.
* The number of hours that the recovery point objective (RPO) is not met is not getting updated in the health report.
* The configuration server is not syncing with RX when the ESX hardware details or network details contain any UTF-8 characters.
* Windows Server 2008 R2 domain controllers fail to boot after recovery.
* Offline sync is not working as expected.
* After virtual machine (VM) failover, replication-pair deletion gets stuck in the CX UI for a long time, and users cannot complete the failback or resume operation.
* Overall snapshot operations that are done by the consistency job have been optimized to help reduce application disconnects like SQL clients.
* The performance of the consistency tool (VACP.exe) has been improved by reducing the memory usage that is required for creating snapshots on Windows.
* The push install service crashes when the password is greater than 16 characters.
* vContinuum is not checking and prompting for new vCenter credentials when the credentials are changed.
* On Linux, the master target cache manager (cachemgr) is not downloading files from the process server, which results in replication pair throttling.
* When the physical failover cluster (MSCS) disk order is not the same on all the nodes, replication is not set for some of the cluster volumes.
  <br/>Note that the cluster needs to be reprotected to take advantage of this fix.  
* SMTP functionality is not working as expected after RX is upgraded from Scout 7.1 to Scout 8.0.1.
* More stats have been added in the log for the rollback operation to track the time it has taken to complete it.
* Support has been added for Linux operating systems on the source server:
  * Red Hat Enterprise Linux (RHEL) 6 update 7
  * CentOS 6 update 7
* The CX and RX UI can now show the notification for the pair, which goes into bitmap mode.
* The following security fixes have been added in RX:

| **Issue description** | **Implementation procedures** |
| --- | --- |
| Authorization bypass via parameter tampering |Restricted access to non-applicable users. |
| Cross-site request forgery |Implemented the page-token concept, which generates randomly for every page. <br/>With this, you will see: <li> There is only a single sign-in instance for the same user.</li><li>Page refresh does not work--it will redirect to the dashboard.</li> |
| Malicious file upload |Restricted files to certain extensions. Allowed extensions are: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml, and zip. |
| Persistent cross-site scripting |Added input validations. |

> [!NOTE]
> * All Site Recovery updates are cumulative. Update 3 has all the fixes of Update 1 and Update 2. Update 3 can be directly applied on 8.0.1 GA.
> * The configuration server and RX updates can’t be rolled back after they're applied on the system.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Update 2 (Update 03Dec15)
Fixes in Update 2 include:

* **Configuration server**: Fix for an issue that prevented the 31-day free metering feature from working as expected when the configuration server was registered in Site Recovery.
* **Unified agent**: Fix for an issue in Update 1 that resulted in the update not being installed on the master target server when it was upgraded from version 8.0 to 8.0.1.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Update 1
Update 1 includes the following bug fixes and new features:

* 31 days of free protection per server instance. This enables you to test functionality or set up a proof-of-concept.
  * All operations on the server, including failover and failback, are free for the first 31 days, starting from the time that a server is first protected with Site Recovery Scout.
  * From the 32nd day onwards, each protected server will be charged at the standard instance rate for Azure Site Recovery protection to a customer-owned site.
  * At any time, the number of protected servers that are currently being charged is available on the Dashboard page of the Azure Site Recovery vault.
* Support added for vSphere Command-Line Interface (vCLI) 5.5 Update 2.
* Support added for Linux operating systems on the source server:
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Bug fixes to address the following issues:
  * Vault registration fails for the configuration server or RX server.
  * Cluster volumes don't appear as expected when clustered virtual machines are reprotected when they resume.
  * Failback fails when the master target server is hosted on a different ESXi server from the on-premises production virtual machines.
  * Configuration file permissions are changed when you upgrade to 8.0.1, which affects protection and operations.
  * The resynchronization threshold isn't enforced as expected, which leads to inconsistent replication behavior.
  * The RPO settings are not appearing correctly in the configuration server interface. The uncompressed data value incorrectly shows the compressed value.
  * The Remove operation doesn't delete as expected in the vContinuum wizard, and replication isn't deleted from the configuration server interface.
  * In the vContinuum wizard, the disk is automatically unselected when you click **Details** in the disk view during protection of MSCS virtual machines.
  * During the physical-to-virtual (P2V) scenario, required HP services, such as CIMnotify and CqMgHost, aren't moved to manual in virtual machine recovery. This results in additional boot time.
  * Linux virtual machine protection fails when there are more than 26 disks on the master target server.

## <a name="next-steps"></a>Next steps
Post any questions that you have on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
