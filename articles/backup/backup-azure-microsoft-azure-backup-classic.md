---
title: Use Azure Backup Server to back up workloads to Azure classic portal | Microsoft Docs
description: Make sure your environment is properly prepared to back up workloads using Azure Backup Server
services: backup
documentationcenter: ''
author: pvrk
manager: shivamg
editor: ''
keywords: azure backup server; backup vault
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: eeaeff25e8dc696ece390b94a016614e066bb44b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554749"
---
# <a name="preparing-to-back-up-workloads-using-azure-backup-server"></a><span data-ttu-id="6a2e5-104">Preparing to back up workloads using Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="6a2e5-104">Preparing to back up workloads using Azure Backup Server</span></span>
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (Classic)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Classic)](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="6a2e5-109">This article is about preparing your environment to back up workloads using Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-109">This article is about preparing your environment to back up workloads using Azure Backup Server.</span></span> <span data-ttu-id="6a2e5-110">With Azure Backup Server, you can protect application workloads such as Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange and Windows clients from a single console.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-110">With Azure Backup Server, you can protect application workloads such as Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange and Windows clients from a single console.</span></span>

> [!WARNING]
> Azure Backup Server inherits the functionality of Data Protection Manager (DPM) for workload backup. You will find pointers to DPM documentation for some of these capabilities. However Azure Backup Server does not provide protection on tape or integrate with System Center.
>
>

## <a name="1-windows-server-machine"></a><span data-ttu-id="6a2e5-114">1. Windows Server machine</span><span class="sxs-lookup"><span data-stu-id="6a2e5-114">1. Windows Server machine</span></span>
![step1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/step1.png)

<span data-ttu-id="6a2e5-116">The first step towards getting the Azure Backup Server up and running is to have a Windows Server machine.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-116">The first step towards getting the Azure Backup Server up and running is to have a Windows Server machine.</span></span>

| <span data-ttu-id="6a2e5-117">Location</span><span class="sxs-lookup"><span data-stu-id="6a2e5-117">Location</span></span> | <span data-ttu-id="6a2e5-118">Minimum requirements</span><span class="sxs-lookup"><span data-stu-id="6a2e5-118">Minimum requirements</span></span> | <span data-ttu-id="6a2e5-119">Additional instructions</span><span class="sxs-lookup"><span data-stu-id="6a2e5-119">Additional instructions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a2e5-120">Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e5-120">Azure</span></span> |<span data-ttu-id="6a2e5-121">Azure IaaS virtual machine</span><span class="sxs-lookup"><span data-stu-id="6a2e5-121">Azure IaaS virtual machine</span></span><br><br><span data-ttu-id="6a2e5-122">A2 Standard: 2 cores, 3.5GB RAM</span><span class="sxs-lookup"><span data-stu-id="6a2e5-122">A2 Standard: 2 cores, 3.5GB RAM</span></span> |<span data-ttu-id="6a2e5-123">You can start with a simple gallery image of Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-123">You can start with a simple gallery image of Windows Server 2012 R2 Datacenter.</span></span> <span data-ttu-id="6a2e5-124">[Protecting IaaS workloads using Azure Backup Server (DPM)](https://technet.microsoft.com/library/jj852163.aspx) has many nuances.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-124">[Protecting IaaS workloads using Azure Backup Server (DPM)](https://technet.microsoft.com/library/jj852163.aspx) has many nuances.</span></span> <span data-ttu-id="6a2e5-125">Ensure that you read the article completely before deploying the machine.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-125">Ensure that you read the article completely before deploying the machine.</span></span> |
| <span data-ttu-id="6a2e5-126">On-premises</span><span class="sxs-lookup"><span data-stu-id="6a2e5-126">On-premises</span></span> |<span data-ttu-id="6a2e5-127">Hyper-V VM,</span><span class="sxs-lookup"><span data-stu-id="6a2e5-127">Hyper-V VM,</span></span><br> <span data-ttu-id="6a2e5-128">VMWare VM,</span><span class="sxs-lookup"><span data-stu-id="6a2e5-128">VMWare VM,</span></span><br> <span data-ttu-id="6a2e5-129">or a physical host</span><span class="sxs-lookup"><span data-stu-id="6a2e5-129">or a physical host</span></span><br><br><span data-ttu-id="6a2e5-130">2 cores and 4GB RAM</span><span class="sxs-lookup"><span data-stu-id="6a2e5-130">2 cores and 4GB RAM</span></span> |<span data-ttu-id="6a2e5-131">You can deduplicate the DPM storage using Windows Server Deduplication.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-131">You can deduplicate the DPM storage using Windows Server Deduplication.</span></span> <span data-ttu-id="6a2e5-132">Learn more about how [DPM and deduplication](https://technet.microsoft.com/library/dn891438.aspx) work together when deployed in Hyper-V VMs.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-132">Learn more about how [DPM and deduplication](https://technet.microsoft.com/library/dn891438.aspx) work together when deployed in Hyper-V VMs.</span></span> |

> [!NOTE]
> It is recommended that Azure Backup Server be installed on a machine with Windows Server 2012 R2 Datacenter. A lot of the prerequisites are automatically covered with the latest version of the Windows operating system.
>
>

<span data-ttu-id="6a2e5-135">If you plan to join Azure Backup Server to a domain, it is recommended that you join the physical server or virtual machine to the domain before installing the Azure Backup Server software.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-135">If you plan to join Azure Backup Server to a domain, it is recommended that you join the physical server or virtual machine to the domain before installing the Azure Backup Server software.</span></span> <span data-ttu-id="6a2e5-136">Moving an Azure Backup Server to a new domain, after deployment, is *not supported*.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-136">Moving an Azure Backup Server to a new domain, after deployment, is *not supported*.</span></span>

## <a name="2-backup-vault"></a><span data-ttu-id="6a2e5-137">2. Backup vault</span><span class="sxs-lookup"><span data-stu-id="6a2e5-137">2. Backup vault</span></span>
![step2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/step2.png)

<span data-ttu-id="6a2e5-139">Whether you send backup data to Azure or keep it locally, the Azure Backup Server must be registered to a vault.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-139">Whether you send backup data to Azure or keep it locally, the Azure Backup Server must be registered to a vault.</span></span>

> [!IMPORTANT]
> Starting March 2017, you can no longer use the classic portal to create Backup vaults. Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault). However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.
>
>



## <a name="3-software-package"></a><span data-ttu-id="6a2e5-143">3. Software package</span><span class="sxs-lookup"><span data-stu-id="6a2e5-143">3. Software package</span></span>
![step3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-the-software-package"></a><span data-ttu-id="6a2e5-145">Downloading the software package</span><span class="sxs-lookup"><span data-stu-id="6a2e5-145">Downloading the software package</span></span>
<span data-ttu-id="6a2e5-146">Similar to vault credentials, you can download Microsoft Azure Backup for application workloads from the **Quick Start Page** of the backup vault.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-146">Similar to vault credentials, you can download Microsoft Azure Backup for application workloads from the **Quick Start Page** of the backup vault.</span></span>

1. <span data-ttu-id="6a2e5-147">Click **For Application Workloads (Disk to Disk to Cloud)**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-147">Click **For Application Workloads (Disk to Disk to Cloud)**.</span></span> <span data-ttu-id="6a2e5-148">This will take you to the Download Center page from where the software package can be downloaded.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-148">This will take you to the Download Center page from where the software package can be downloaded.</span></span>

    ![Microsoft Azure Backup Welcome Screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. <span data-ttu-id="6a2e5-150">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-150">Click **Download**.</span></span>

    ![Download center 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. <span data-ttu-id="6a2e5-152">Select all the files and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-152">Select all the files and click **Next**.</span></span> <span data-ttu-id="6a2e5-153">Download all the files coming in from the Microsoft Azure Backup download page, and place all the files in the same folder.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-153">Download all the files coming in from the Microsoft Azure Backup download page, and place all the files in the same folder.</span></span>
   <span data-ttu-id="6a2e5-154">![Download center 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/downloadcenter.png)</span><span class="sxs-lookup"><span data-stu-id="6a2e5-154">![Download center 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/downloadcenter.png)</span></span>

    <span data-ttu-id="6a2e5-155">Since the download size of all the files together is > 3G, on a 10Mbps download link it may take up to 60 minutes for the download to complete.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-155">Since the download size of all the files together is > 3G, on a 10Mbps download link it may take up to 60 minutes for the download to complete.</span></span>

### <a name="extracting-the-software-package"></a><span data-ttu-id="6a2e5-156">Extracting the software package</span><span class="sxs-lookup"><span data-stu-id="6a2e5-156">Extracting the software package</span></span>
<span data-ttu-id="6a2e5-157">After you've downloaded all the files, click **MicrosoftAzureBackupInstaller.exe**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-157">After you've downloaded all the files, click **MicrosoftAzureBackupInstaller.exe**.</span></span> <span data-ttu-id="6a2e5-158">This will start the **Microsoft Azure Backup Setup Wizard** to extract the setup files to a location specified by you.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-158">This will start the **Microsoft Azure Backup Setup Wizard** to extract the setup files to a location specified by you.</span></span> <span data-ttu-id="6a2e5-159">Continue through the wizard and click on the **Extract** button to begin the extraction process.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-159">Continue through the wizard and click on the **Extract** button to begin the extraction process.</span></span>

> [!WARNING]
> At least 4GB of free space is required to extract the setup files.
>
>

![Microsoft Azure Backup Setup Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/extract/03.png)

<span data-ttu-id="6a2e5-162">Once the extraction process complete, check the box to launch the freshly extracted *setup.exe* to begin installing Microsoft Azure Backup Server and click on the **Finish** button.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-162">Once the extraction process complete, check the box to launch the freshly extracted *setup.exe* to begin installing Microsoft Azure Backup Server and click on the **Finish** button.</span></span>

### <a name="installing-the-software-package"></a><span data-ttu-id="6a2e5-163">Installing the software package</span><span class="sxs-lookup"><span data-stu-id="6a2e5-163">Installing the software package</span></span>
1. <span data-ttu-id="6a2e5-164">Click **Microsoft Azure Backup** to launch the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-164">Click **Microsoft Azure Backup** to launch the setup wizard.</span></span>

    ![Microsoft Azure Backup Setup Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. <span data-ttu-id="6a2e5-166">On the Welcome screen click the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-166">On the Welcome screen click the **Next** button.</span></span> <span data-ttu-id="6a2e5-167">This takes you to the *Prerequisite Checks* section.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-167">This takes you to the *Prerequisite Checks* section.</span></span> <span data-ttu-id="6a2e5-168">On this screen, click on the **Check** button to determine if the hardware and software prerequisites for Azure Backup Server have been met.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-168">On this screen, click on the **Check** button to determine if the hardware and software prerequisites for Azure Backup Server have been met.</span></span> <span data-ttu-id="6a2e5-169">If all of the prerequisites are have been met successfully, you will see a message indicating that the machine meets the requirements.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-169">If all of the prerequisites are have been met successfully, you will see a message indicating that the machine meets the requirements.</span></span> <span data-ttu-id="6a2e5-170">Click on the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-170">Click on the **Next** button.</span></span>

    ![Azure Backup Server - Welcome and Prerequisites check](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. <span data-ttu-id="6a2e5-172">Microsoft Azure Backup Server requires SQL Server Standard, and the Azure Backup Server installation package comes bundled with the appropriate SQL Server binaries needed.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-172">Microsoft Azure Backup Server requires SQL Server Standard, and the Azure Backup Server installation package comes bundled with the appropriate SQL Server binaries needed.</span></span> <span data-ttu-id="6a2e5-173">When starting with a new Azure Backup Server installation, you should pick the option **Install new Instance of SQL Server with this Setup** and click the **Check and Install** button.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-173">When starting with a new Azure Backup Server installation, you should pick the option **Install new Instance of SQL Server with this Setup** and click the **Check and Install** button.</span></span> <span data-ttu-id="6a2e5-174">Once the prerequisites are successfully installed, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-174">Once the prerequisites are successfully installed, click **Next**.</span></span>

    ![Azure Backup Server - SQL check](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/sql/01.png)

    <span data-ttu-id="6a2e5-176">If a failure occurs with a recommendation to restart the machine, do so and click **Check Again**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-176">If a failure occurs with a recommendation to restart the machine, do so and click **Check Again**.</span></span>

   > [!NOTE]
   > Azure Backup Server will not work with a remote SQL Server instance. The instance being used by Azure Backup Server needs to be local.
   >
   >

4. <span data-ttu-id="6a2e5-179">Provide a location for the installation of Microsoft Azure Backup server files and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-179">Provide a location for the installation of Microsoft Azure Backup server files and click **Next**.</span></span>

    ![Microsoft Azure Backup PreReq2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/space-screen.png)

    <span data-ttu-id="6a2e5-181">The scratch location is a requirement for back up to Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-181">The scratch location is a requirement for back up to Azure.</span></span> <span data-ttu-id="6a2e5-182">Ensure the scratch location is at least 5% of the data planned to be backed up to the cloud.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-182">Ensure the scratch location is at least 5% of the data planned to be backed up to the cloud.</span></span> <span data-ttu-id="6a2e5-183">For disk protection, separate disks need to be configured once the installation completes.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-183">For disk protection, separate disks need to be configured once the installation completes.</span></span> <span data-ttu-id="6a2e5-184">For more information regarding storage pools, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a2e5-184">For more information regarding storage pools, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span></span>
5. <span data-ttu-id="6a2e5-185">Provide a strong password for restricted local user accounts and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-185">Provide a strong password for restricted local user accounts and click **Next**.</span></span>

    ![Microsoft Azure Backup PreReq2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/security-screen.png)
6. <span data-ttu-id="6a2e5-187">Select whether you want to use *Microsoft Update* to check for updates and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-187">Select whether you want to use *Microsoft Update* to check for updates and click **Next**.</span></span>

   > [!NOTE]
   > We recommend having Windows Update redirect to Microsoft Update, which offers security and important updates for Windows and other products like Microsoft Azure Backup Server.
   >
   >

    ![Microsoft Azure Backup PreReq2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. <span data-ttu-id="6a2e5-190">Review the *Summary of Settings* and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-190">Review the *Summary of Settings* and click **Install**.</span></span>

    ![Microsoft Azure Backup PreReq2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. <span data-ttu-id="6a2e5-192">The installation happens in phases.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-192">The installation happens in phases.</span></span> <span data-ttu-id="6a2e5-193">In the first phase the Microsoft Azure Recovery Services Agent is installed on the server.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-193">In the first phase the Microsoft Azure Recovery Services Agent is installed on the server.</span></span> <span data-ttu-id="6a2e5-194">The wizard also checks for Internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-194">The wizard also checks for Internet connectivity.</span></span> <span data-ttu-id="6a2e5-195">If Internet connectivity is available you can proceed with installation, if not, you need to provide proxy details to connect to the Internet.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-195">If Internet connectivity is available you can proceed with installation, if not, you need to provide proxy details to connect to the Internet.</span></span>

    <span data-ttu-id="6a2e5-196">The next step is to configure the Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-196">The next step is to configure the Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="6a2e5-197">As a part of the configuration, you will have to provide your the vault credentials to register the machine to the backup vault.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-197">As a part of the configuration, you will have to provide your the vault credentials to register the machine to the backup vault.</span></span> <span data-ttu-id="6a2e5-198">You will also provide a passphrase to encrypt/decrypt the data sent between Azure and your premises.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-198">You will also provide a passphrase to encrypt/decrypt the data sent between Azure and your premises.</span></span> <span data-ttu-id="6a2e5-199">You can automatically generate a passphrase or provide your own minimum 16-character passphrase.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-199">You can automatically generate a passphrase or provide your own minimum 16-character passphrase.</span></span> <span data-ttu-id="6a2e5-200">Continue with the wizard until the agent has been configured.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-200">Continue with the wizard until the agent has been configured.</span></span>

    ![Azure Backup Serer PreReq2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/mars/04.png)
9. <span data-ttu-id="6a2e5-202">Once registration of the Microsoft Azure Backup server successfully completes, the overall setup wizard proceeds to the installation and configuration of SQL Server and the Azure Backup Server components.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-202">Once registration of the Microsoft Azure Backup server successfully completes, the overall setup wizard proceeds to the installation and configuration of SQL Server and the Azure Backup Server components.</span></span> <span data-ttu-id="6a2e5-203">Once the SQL Server component installation completes, the Azure Backup Server components are installed.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-203">Once the SQL Server component installation completes, the Azure Backup Server components are installed.</span></span>

    ![Azure Backup Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

<span data-ttu-id="6a2e5-205">When the installation step has completed, the product's desktop icons will have been created as well.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-205">When the installation step has completed, the product's desktop icons will have been created as well.</span></span> <span data-ttu-id="6a2e5-206">Just double-click the icon to launch the product.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-206">Just double-click the icon to launch the product.</span></span>

### <a name="add-backup-storage"></a><span data-ttu-id="6a2e5-207">Add backup storage</span><span class="sxs-lookup"><span data-stu-id="6a2e5-207">Add backup storage</span></span>
<span data-ttu-id="6a2e5-208">The first backup copy is kept on storage attached to the Azure Backup Server machine.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-208">The first backup copy is kept on storage attached to the Azure Backup Server machine.</span></span> <span data-ttu-id="6a2e5-209">For more information about adding disks, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a2e5-209">For more information about adding disks, see [Configure storage pools and disk storage](https://technet.microsoft.com/library/hh758075.aspx).</span></span>

> [!NOTE]
> You need to add backup storage even if you plan to send data to Azure. In the current architecture of Azure Backup Server, the Azure Backup vault holds the *second* copy of the data while the local storage holds the first (and mandatory) backup copy.  
>
>

## <a name="4-network-connectivity"></a><span data-ttu-id="6a2e5-212">4. Network connectivity</span><span class="sxs-lookup"><span data-stu-id="6a2e5-212">4. Network connectivity</span></span>
![step4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-microsoft-azure-backup/step4.png)

<span data-ttu-id="6a2e5-214">Azure Backup Server requires connectivity to the Azure Backup service for the product to work successfully.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-214">Azure Backup Server requires connectivity to the Azure Backup service for the product to work successfully.</span></span> <span data-ttu-id="6a2e5-215">To validate whether the machine has the connectivity to Azure, use the ```Get-DPMCloudConnection``` commandlet in the Azure Backup Server PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-215">To validate whether the machine has the connectivity to Azure, use the ```Get-DPMCloudConnection``` commandlet in the Azure Backup Server PowerShell console.</span></span> <span data-ttu-id="6a2e5-216">If the output of the commandlet is TRUE then connectivity exists, else there is no connectivity.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-216">If the output of the commandlet is TRUE then connectivity exists, else there is no connectivity.</span></span>

<span data-ttu-id="6a2e5-217">At the same time, the Azure subscription needs to be in a healthy state.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-217">At the same time, the Azure subscription needs to be in a healthy state.</span></span> <span data-ttu-id="6a2e5-218">To find out the state of your subscription and to manage it, log in to the [subscription portal](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="6a2e5-218">To find out the state of your subscription and to manage it, log in to the [subscription portal](https://account.windowsazure.com/Subscriptions).</span></span>

<span data-ttu-id="6a2e5-219">Once you know the state of the Azure connectivity and of the Azure subscription, you can use the table below to find out the impact on the backup/restore functionality offered.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-219">Once you know the state of the Azure connectivity and of the Azure subscription, you can use the table below to find out the impact on the backup/restore functionality offered.</span></span>

| <span data-ttu-id="6a2e5-220">Connectivity State</span><span class="sxs-lookup"><span data-stu-id="6a2e5-220">Connectivity State</span></span> | <span data-ttu-id="6a2e5-221">Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="6a2e5-221">Azure Subscription</span></span> | <span data-ttu-id="6a2e5-222">Backup to Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e5-222">Backup to Azure</span></span> | <span data-ttu-id="6a2e5-223">Backup to disk</span><span class="sxs-lookup"><span data-stu-id="6a2e5-223">Backup to disk</span></span> | <span data-ttu-id="6a2e5-224">Restore from Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e5-224">Restore from Azure</span></span> | <span data-ttu-id="6a2e5-225">Restore from disk</span><span class="sxs-lookup"><span data-stu-id="6a2e5-225">Restore from disk</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6a2e5-226">Connected</span><span class="sxs-lookup"><span data-stu-id="6a2e5-226">Connected</span></span> |<span data-ttu-id="6a2e5-227">Active</span><span class="sxs-lookup"><span data-stu-id="6a2e5-227">Active</span></span> |<span data-ttu-id="6a2e5-228">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-228">Allowed</span></span> |<span data-ttu-id="6a2e5-229">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-229">Allowed</span></span> |<span data-ttu-id="6a2e5-230">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-230">Allowed</span></span> |<span data-ttu-id="6a2e5-231">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-231">Allowed</span></span> |
| <span data-ttu-id="6a2e5-232">Connected</span><span class="sxs-lookup"><span data-stu-id="6a2e5-232">Connected</span></span> |<span data-ttu-id="6a2e5-233">Expired</span><span class="sxs-lookup"><span data-stu-id="6a2e5-233">Expired</span></span> |<span data-ttu-id="6a2e5-234">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-234">Stopped</span></span> |<span data-ttu-id="6a2e5-235">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-235">Stopped</span></span> |<span data-ttu-id="6a2e5-236">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-236">Allowed</span></span> |<span data-ttu-id="6a2e5-237">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-237">Allowed</span></span> |
| <span data-ttu-id="6a2e5-238">Connected</span><span class="sxs-lookup"><span data-stu-id="6a2e5-238">Connected</span></span> |<span data-ttu-id="6a2e5-239">Deprovisioned</span><span class="sxs-lookup"><span data-stu-id="6a2e5-239">Deprovisioned</span></span> |<span data-ttu-id="6a2e5-240">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-240">Stopped</span></span> |<span data-ttu-id="6a2e5-241">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-241">Stopped</span></span> |<span data-ttu-id="6a2e5-242">Stopped and Azure recovery points deleted</span><span class="sxs-lookup"><span data-stu-id="6a2e5-242">Stopped and Azure recovery points deleted</span></span> |<span data-ttu-id="6a2e5-243">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-243">Stopped</span></span> |
| <span data-ttu-id="6a2e5-244">Lost connectivity > 15 days</span><span class="sxs-lookup"><span data-stu-id="6a2e5-244">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6a2e5-245">Active</span><span class="sxs-lookup"><span data-stu-id="6a2e5-245">Active</span></span> |<span data-ttu-id="6a2e5-246">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-246">Stopped</span></span> |<span data-ttu-id="6a2e5-247">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-247">Stopped</span></span> |<span data-ttu-id="6a2e5-248">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-248">Allowed</span></span> |<span data-ttu-id="6a2e5-249">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-249">Allowed</span></span> |
| <span data-ttu-id="6a2e5-250">Lost connectivity > 15 days</span><span class="sxs-lookup"><span data-stu-id="6a2e5-250">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6a2e5-251">Expired</span><span class="sxs-lookup"><span data-stu-id="6a2e5-251">Expired</span></span> |<span data-ttu-id="6a2e5-252">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-252">Stopped</span></span> |<span data-ttu-id="6a2e5-253">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-253">Stopped</span></span> |<span data-ttu-id="6a2e5-254">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-254">Allowed</span></span> |<span data-ttu-id="6a2e5-255">Allowed</span><span class="sxs-lookup"><span data-stu-id="6a2e5-255">Allowed</span></span> |
| <span data-ttu-id="6a2e5-256">Lost connectivity > 15 days</span><span class="sxs-lookup"><span data-stu-id="6a2e5-256">Lost connectivity > 15 days</span></span> |<span data-ttu-id="6a2e5-257">Deprovisioned</span><span class="sxs-lookup"><span data-stu-id="6a2e5-257">Deprovisioned</span></span> |<span data-ttu-id="6a2e5-258">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-258">Stopped</span></span> |<span data-ttu-id="6a2e5-259">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-259">Stopped</span></span> |<span data-ttu-id="6a2e5-260">Stopped and Azure recovery points deleted</span><span class="sxs-lookup"><span data-stu-id="6a2e5-260">Stopped and Azure recovery points deleted</span></span> |<span data-ttu-id="6a2e5-261">Stopped</span><span class="sxs-lookup"><span data-stu-id="6a2e5-261">Stopped</span></span> |

### <a name="recovering-from-loss-of-connectivity"></a><span data-ttu-id="6a2e5-262">Recovering from loss of connectivity</span><span class="sxs-lookup"><span data-stu-id="6a2e5-262">Recovering from loss of connectivity</span></span>
<span data-ttu-id="6a2e5-263">If you have a firewall or a proxy that is preventing access to Azure, you need to whitelist the following domain addresses in the firewall/proxy profile:</span><span class="sxs-lookup"><span data-stu-id="6a2e5-263">If you have a firewall or a proxy that is preventing access to Azure, you need to whitelist the following domain addresses in the firewall/proxy profile:</span></span>

* <span data-ttu-id="6a2e5-264">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6a2e5-264">www.msftncsi.com</span></span>
* <span data-ttu-id="6a2e5-265">\*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6a2e5-265">\*.Microsoft.com</span></span>
* <span data-ttu-id="6a2e5-266">\*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="6a2e5-266">\*.WindowsAzure.com</span></span>
* <span data-ttu-id="6a2e5-267">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6a2e5-267">\*.microsoftonline.com</span></span>
* <span data-ttu-id="6a2e5-268">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="6a2e5-268">\*.windows.net</span></span>

<span data-ttu-id="6a2e5-269">Once connectivity to Azure has been restored to the Azure Backup Server machine, the operations that can be performed are determined by the Azure subscription state.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-269">Once connectivity to Azure has been restored to the Azure Backup Server machine, the operations that can be performed are determined by the Azure subscription state.</span></span> <span data-ttu-id="6a2e5-270">The table above has details about the operations allowed once the machine is "Connected".</span><span class="sxs-lookup"><span data-stu-id="6a2e5-270">The table above has details about the operations allowed once the machine is "Connected".</span></span>

### <a name="handling-subscription-states"></a><span data-ttu-id="6a2e5-271">Handling subscription states</span><span class="sxs-lookup"><span data-stu-id="6a2e5-271">Handling subscription states</span></span>
<span data-ttu-id="6a2e5-272">It is possible to take an Azure subscription from an *Expired* or *Deprovisioned* state to the *Active* state.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-272">It is possible to take an Azure subscription from an *Expired* or *Deprovisioned* state to the *Active* state.</span></span> <span data-ttu-id="6a2e5-273">However this has some implications on the product behavior while the state is not *Active*:</span><span class="sxs-lookup"><span data-stu-id="6a2e5-273">However this has some implications on the product behavior while the state is not *Active*:</span></span>

* <span data-ttu-id="6a2e5-274">A *Deprovisioned* subscription loses functionality for the period that it is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-274">A *Deprovisioned* subscription loses functionality for the period that it is deprovisioned.</span></span> <span data-ttu-id="6a2e5-275">On turning *Active*, the product functionality of backup/restore is revived.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-275">On turning *Active*, the product functionality of backup/restore is revived.</span></span> <span data-ttu-id="6a2e5-276">The backup data on the local disk also can be retrieved if it was kept with a sufficiently large retention period.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-276">The backup data on the local disk also can be retrieved if it was kept with a sufficiently large retention period.</span></span> <span data-ttu-id="6a2e5-277">However, the backup data in Azure is irretrievably lost once the subscription enters the *Deprovisioned* state.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-277">However, the backup data in Azure is irretrievably lost once the subscription enters the *Deprovisioned* state.</span></span>
* <span data-ttu-id="6a2e5-278">An *Expired* subscription only loses functionality for until it has been made *Active* again.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-278">An *Expired* subscription only loses functionality for until it has been made *Active* again.</span></span> <span data-ttu-id="6a2e5-279">Any backups scheduled for the period that the subscription was *Expired* will not run.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-279">Any backups scheduled for the period that the subscription was *Expired* will not run.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6a2e5-280">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="6a2e5-280">Troubleshooting</span></span>
<span data-ttu-id="6a2e5-281">If Microsoft Azure Backup server fails with errors during the setup phase (or backup or restore), refer to this [error codes document](https://support.microsoft.com/kb/3041338)  for more information.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-281">If Microsoft Azure Backup server fails with errors during the setup phase (or backup or restore), refer to this [error codes document](https://support.microsoft.com/kb/3041338)  for more information.</span></span>
<span data-ttu-id="6a2e5-282">You can also refer to [Azure Backup related FAQs](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6a2e5-282">You can also refer to [Azure Backup related FAQs](backup-azure-backup-faq.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a2e5-283">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a2e5-283">Next steps</span></span>
<span data-ttu-id="6a2e5-284">You can get detailed information about [preparing your environment for DPM](https://technet.microsoft.com/library/hh758176.aspx) on the Microsoft TechNet site.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-284">You can get detailed information about [preparing your environment for DPM](https://technet.microsoft.com/library/hh758176.aspx) on the Microsoft TechNet site.</span></span> <span data-ttu-id="6a2e5-285">It also contains information about supported configurations on which Azure Backup Server can be deployed and used.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-285">It also contains information about supported configurations on which Azure Backup Server can be deployed and used.</span></span>

<span data-ttu-id="6a2e5-286">You can use these articles to gain a deeper understanding of workload protection using Microsoft Azure Backup server.</span><span class="sxs-lookup"><span data-stu-id="6a2e5-286">You can use these articles to gain a deeper understanding of workload protection using Microsoft Azure Backup server.</span></span>

* [<span data-ttu-id="6a2e5-287">SQL Server backup</span><span class="sxs-lookup"><span data-stu-id="6a2e5-287">SQL Server backup</span></span>](backup-azure-backup-sql.md)
* [<span data-ttu-id="6a2e5-288">SharePoint server backup</span><span class="sxs-lookup"><span data-stu-id="6a2e5-288">SharePoint server backup</span></span>](backup-azure-backup-sharepoint.md)
* [<span data-ttu-id="6a2e5-289">Alternate server backup</span><span class="sxs-lookup"><span data-stu-id="6a2e5-289">Alternate server backup</span></span>](backup-azure-alternate-dpm-server.md)

















