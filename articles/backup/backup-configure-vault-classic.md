---
title: Back up Windows server or workstation to Azure (classic model) | Microsoft Docs
description: Backup Windows servers or clients to a backup vault in Azure. Go through basics for protecting files and folders to a Backup vault by using the Azure Backup agent.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: backup vault; back up a Windows server; backup windows;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 1015efcd03115b1aa90c9ecddf4c304754262390
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551666"
---
# <a name="back-up-a-windows-server-or-workstation-to-azure-using-the-classic-portal"></a><span data-ttu-id="69122-105">Back up a Windows server or workstation to Azure using the classic portal</span><span class="sxs-lookup"><span data-stu-id="69122-105">Back up a Windows server or workstation to Azure using the classic portal</span></span>
> [!div class="op_single_selector"]
> * [Classic portal](backup-configure-vault-classic.md)
> * [Azure portal](backup-configure-vault.md)
>
>

<span data-ttu-id="69122-108">This article covers the procedures that you need to follow to prepare your environment and back up a Windows server (or workstation) to Azure.</span><span class="sxs-lookup"><span data-stu-id="69122-108">This article covers the procedures that you need to follow to prepare your environment and back up a Windows server (or workstation) to Azure.</span></span> <span data-ttu-id="69122-109">It also covers considerations for deploying your backup solution.</span><span class="sxs-lookup"><span data-stu-id="69122-109">It also covers considerations for deploying your backup solution.</span></span> <span data-ttu-id="69122-110">If you're interested in trying Azure Backup for the first time, this article quickly walks you through the process.</span><span class="sxs-lookup"><span data-stu-id="69122-110">If you're interested in trying Azure Backup for the first time, this article quickly walks you through the process.</span></span>


> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: Resource Manager and classic. This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.
>
>

## <a name="before-you-start"></a><span data-ttu-id="69122-114">Before you start</span><span class="sxs-lookup"><span data-stu-id="69122-114">Before you start</span></span>
<span data-ttu-id="69122-115">To back up a server or client to Azure, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="69122-115">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="69122-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="69122-116">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-backup-vault"></a><span data-ttu-id="69122-117">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="69122-117">Create a backup vault</span></span>
<span data-ttu-id="69122-118">To back up files and folders from a server or client, you need to create a backup vault in the geographic region where you want to store the data.</span><span class="sxs-lookup"><span data-stu-id="69122-118">To back up files and folders from a server or client, you need to create a backup vault in the geographic region where you want to store the data.</span></span>

> [!IMPORTANT]
> Starting March 2017, you can no longer use the classic portal to create Backup vaults. Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault). However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.


## <a name="download-the-vault-credential-file"></a><span data-ttu-id="69122-122">Download the vault credential file</span><span class="sxs-lookup"><span data-stu-id="69122-122">Download the vault credential file</span></span>
<span data-ttu-id="69122-123">The on-premises machine needs to be authenticated with a backup vault before it can back up data to Azure.</span><span class="sxs-lookup"><span data-stu-id="69122-123">The on-premises machine needs to be authenticated with a backup vault before it can back up data to Azure.</span></span> <span data-ttu-id="69122-124">The authentication is achieved through *vault credentials*.</span><span class="sxs-lookup"><span data-stu-id="69122-124">The authentication is achieved through *vault credentials*.</span></span> <span data-ttu-id="69122-125">The vault credential file is downloaded through a secure channel from the classic portal.</span><span class="sxs-lookup"><span data-stu-id="69122-125">The vault credential file is downloaded through a secure channel from the classic portal.</span></span> <span data-ttu-id="69122-126">The certificate private key does not persist in the portal or the service.</span><span class="sxs-lookup"><span data-stu-id="69122-126">The certificate private key does not persist in the portal or the service.</span></span>

<span data-ttu-id="69122-127">Learn more about [using vault credentials to authenticate with the Backup service](backup-introduction-to-azure-backup.md#what-is-the-vault-credential-file).</span><span class="sxs-lookup"><span data-stu-id="69122-127">Learn more about [using vault credentials to authenticate with the Backup service](backup-introduction-to-azure-backup.md#what-is-the-vault-credential-file).</span></span>

### <a name="to-download-the-vault-credential-file-to-a-local-machine"></a><span data-ttu-id="69122-128">To download the vault credential file to a local machine</span><span class="sxs-lookup"><span data-stu-id="69122-128">To download the vault credential file to a local machine</span></span>
1. <span data-ttu-id="69122-129">In the left navigation pane, click **Recovery Services**, and then select the backup vault that you created.</span><span class="sxs-lookup"><span data-stu-id="69122-129">In the left navigation pane, click **Recovery Services**, and then select the backup vault that you created.</span></span>

    ![IR complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/rs-left-nav.png)
2. <span data-ttu-id="69122-131">On the Quick Start page, click **Download vault credentials**.</span><span class="sxs-lookup"><span data-stu-id="69122-131">On the Quick Start page, click **Download vault credentials**.</span></span>

   <span data-ttu-id="69122-132">The classic portal generates a vault credential by using a combination of the vault name and the current date.</span><span class="sxs-lookup"><span data-stu-id="69122-132">The classic portal generates a vault credential by using a combination of the vault name and the current date.</span></span> <span data-ttu-id="69122-133">The vault credentials file is used only during the registration workflow and expires after 48 hours.</span><span class="sxs-lookup"><span data-stu-id="69122-133">The vault credentials file is used only during the registration workflow and expires after 48 hours.</span></span>

   <span data-ttu-id="69122-134">The vault credential file can be downloaded from the portal.</span><span class="sxs-lookup"><span data-stu-id="69122-134">The vault credential file can be downloaded from the portal.</span></span>
3. <span data-ttu-id="69122-135">Click **Save** to download the vault credential file to the Downloads folder of the local account.</span><span class="sxs-lookup"><span data-stu-id="69122-135">Click **Save** to download the vault credential file to the Downloads folder of the local account.</span></span> <span data-ttu-id="69122-136">You can also select **Save As** from the **Save** menu to specify a location for the vault credential file.</span><span class="sxs-lookup"><span data-stu-id="69122-136">You can also select **Save As** from the **Save** menu to specify a location for the vault credential file.</span></span>

   > [!NOTE]
   > Make sure the vault credential file is saved in a location that can be accessed from your machine. If it is stored in a file share or server message block, verify that you have the permissions to access it.
   >
   >

## <a name="download-install-and-register-the-backup-agent"></a><span data-ttu-id="69122-139">Download, install, and register the Backup agent</span><span class="sxs-lookup"><span data-stu-id="69122-139">Download, install, and register the Backup agent</span></span>
<span data-ttu-id="69122-140">After you create the backup vault and download the vault credential file, an agent must be installed on each of your Windows machines.</span><span class="sxs-lookup"><span data-stu-id="69122-140">After you create the backup vault and download the vault credential file, an agent must be installed on each of your Windows machines.</span></span>

### <a name="to-download-install-and-register-the-agent"></a><span data-ttu-id="69122-141">To download, install, and register the agent</span><span class="sxs-lookup"><span data-stu-id="69122-141">To download, install, and register the agent</span></span>
1. <span data-ttu-id="69122-142">Click **Recovery Services**, and then select the backup vault that you want to register with a server.</span><span class="sxs-lookup"><span data-stu-id="69122-142">Click **Recovery Services**, and then select the backup vault that you want to register with a server.</span></span>
2. <span data-ttu-id="69122-143">On the Quick Start page, click the agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span><span class="sxs-lookup"><span data-stu-id="69122-143">On the Quick Start page, click the agent **Agent for Windows Server or System Center Data Protection Manager or Windows client**.</span></span> <span data-ttu-id="69122-144">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="69122-144">Then click **Save**.</span></span>

    ![Save agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/agent.png)
3. <span data-ttu-id="69122-146">After the MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from the saved location).</span><span class="sxs-lookup"><span data-stu-id="69122-146">After the MARSagentinstaller.exe file has downloaded, click **Run** (or double-click **MARSAgentInstaller.exe** from the saved location).</span></span>
4. <span data-ttu-id="69122-147">Choose the installation folder and cache folder that are required for the agent, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-147">Choose the installation folder and cache folder that are required for the agent, and then click **Next**.</span></span> <span data-ttu-id="69122-148">The cache location you specify must have free space equal to at least 5 percent of the backup data.</span><span class="sxs-lookup"><span data-stu-id="69122-148">The cache location you specify must have free space equal to at least 5 percent of the backup data.</span></span>
5. <span data-ttu-id="69122-149">You can continue to connect to the Internet through the default proxy settings.</span><span class="sxs-lookup"><span data-stu-id="69122-149">You can continue to connect to the Internet through the default proxy settings.</span></span>             <span data-ttu-id="69122-150">If you use a proxy server to connect to the Internet, on the Proxy Configuration page, select the **Use custom proxy settings** check box, and then enter the proxy server details.</span><span class="sxs-lookup"><span data-stu-id="69122-150">If you use a proxy server to connect to the Internet, on the Proxy Configuration page, select the **Use custom proxy settings** check box, and then enter the proxy server details.</span></span> <span data-ttu-id="69122-151">If you use an authenticated proxy, enter the user name and password details, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-151">If you use an authenticated proxy, enter the user name and password details, and then click **Next**.</span></span>
6. <span data-ttu-id="69122-152">Click **Install** to begin the agent installation.</span><span class="sxs-lookup"><span data-stu-id="69122-152">Click **Install** to begin the agent installation.</span></span> <span data-ttu-id="69122-153">The Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="69122-153">The Backup agent installs .NET Framework 4.5 and Windows PowerShell (if it’s not already installed) to complete the installation.</span></span>
7. <span data-ttu-id="69122-154">After the agent is installed, click **Proceed to Registration** to continue with the workflow.</span><span class="sxs-lookup"><span data-stu-id="69122-154">After the agent is installed, click **Proceed to Registration** to continue with the workflow.</span></span>
8. <span data-ttu-id="69122-155">On the Vault Identification page, browse to and select the vault credential file that you previously downloaded.</span><span class="sxs-lookup"><span data-stu-id="69122-155">On the Vault Identification page, browse to and select the vault credential file that you previously downloaded.</span></span>

    <span data-ttu-id="69122-156">The vault credential file is valid for only 48 hours after it’s downloaded from the portal.</span><span class="sxs-lookup"><span data-stu-id="69122-156">The vault credential file is valid for only 48 hours after it’s downloaded from the portal.</span></span> <span data-ttu-id="69122-157">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in to the portal and download the vault credential file again.</span><span class="sxs-lookup"><span data-stu-id="69122-157">If you encounter an error on this page (such as “Vault credentials file provided has expired”), sign in to the portal and download the vault credential file again.</span></span>

    <span data-ttu-id="69122-158">Ensure that the vault credential file is available in a location that can be accessed by the setup application.</span><span class="sxs-lookup"><span data-stu-id="69122-158">Ensure that the vault credential file is available in a location that can be accessed by the setup application.</span></span> <span data-ttu-id="69122-159">If you encounter access-related errors, copy the vault credential file to a temporary location on the same machine and retry the operation.</span><span class="sxs-lookup"><span data-stu-id="69122-159">If you encounter access-related errors, copy the vault credential file to a temporary location on the same machine and retry the operation.</span></span>

    <span data-ttu-id="69122-160">If you encounter a vault credential error such as “Invalid vault credentials provided," the file is damaged or does not have the latest credentials associated with the recovery service.</span><span class="sxs-lookup"><span data-stu-id="69122-160">If you encounter a vault credential error such as “Invalid vault credentials provided," the file is damaged or does not have the latest credentials associated with the recovery service.</span></span> <span data-ttu-id="69122-161">Retry the operation after downloading a new vault credential file from the portal.</span><span class="sxs-lookup"><span data-stu-id="69122-161">Retry the operation after downloading a new vault credential file from the portal.</span></span> <span data-ttu-id="69122-162">This error can also occur if a user clicks the **Download vault credential** option several times in quick succession.</span><span class="sxs-lookup"><span data-stu-id="69122-162">This error can also occur if a user clicks the **Download vault credential** option several times in quick succession.</span></span> <span data-ttu-id="69122-163">In this case, only the last vault credential file is valid.</span><span class="sxs-lookup"><span data-stu-id="69122-163">In this case, only the last vault credential file is valid.</span></span>
9. <span data-ttu-id="69122-164">On the Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span><span class="sxs-lookup"><span data-stu-id="69122-164">On the Encryption Setting page, you can either generate a passphrase or provide a passphrase (with a minimum of 16 characters).</span></span> <span data-ttu-id="69122-165">Remember to save the passphrase in a secure location.</span><span class="sxs-lookup"><span data-stu-id="69122-165">Remember to save the passphrase in a secure location.</span></span>
10. <span data-ttu-id="69122-166">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="69122-166">Click **Finish**.</span></span> <span data-ttu-id="69122-167">The Register Server Wizard registers the server with Backup.</span><span class="sxs-lookup"><span data-stu-id="69122-167">The Register Server Wizard registers the server with Backup.</span></span>

    > [!WARNING]
    > If you lose or forget the passphrase, Microsoft cannot help you recover the backup data. You own the encryption passphrase, and Microsoft does not have visibility into the passphrase that you use. Save the file in a secure location because it will be required during a recovery operation.
    >
    >

11. <span data-ttu-id="69122-171">After the encryption key is set, leave the **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span><span class="sxs-lookup"><span data-stu-id="69122-171">After the encryption key is set, leave the **Launch Microsoft Azure Recovery Services Agent** check box selected, and then click **Close**.</span></span>

## <a name="complete-the-initial-backup"></a><span data-ttu-id="69122-172">Complete the initial backup</span><span class="sxs-lookup"><span data-stu-id="69122-172">Complete the initial backup</span></span>
<span data-ttu-id="69122-173">The initial backup includes two key tasks:</span><span class="sxs-lookup"><span data-stu-id="69122-173">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="69122-174">Creating the backup schedule</span><span class="sxs-lookup"><span data-stu-id="69122-174">Creating the backup schedule</span></span>
* <span data-ttu-id="69122-175">Backing up files and folders for the first time</span><span class="sxs-lookup"><span data-stu-id="69122-175">Backing up files and folders for the first time</span></span>

<span data-ttu-id="69122-176">After the backup policy completes the initial backup, it creates backup points that you can use if you need to recover the data.</span><span class="sxs-lookup"><span data-stu-id="69122-176">After the backup policy completes the initial backup, it creates backup points that you can use if you need to recover the data.</span></span> <span data-ttu-id="69122-177">The backup policy does this based on the schedule that you define.</span><span class="sxs-lookup"><span data-stu-id="69122-177">The backup policy does this based on the schedule that you define.</span></span>

### <a name="to-schedule-the-backup"></a><span data-ttu-id="69122-178">To schedule the backup</span><span class="sxs-lookup"><span data-stu-id="69122-178">To schedule the backup</span></span>
1. <span data-ttu-id="69122-179">Open the Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="69122-179">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="69122-180">(It will open automatically if you left the **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed the Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="69122-180">(It will open automatically if you left the **Launch Microsoft Azure Recovery Services Agent** check box selected when you closed the Register Server Wizard.) You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Launch the Azure Backup agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/snap-in-search.png)
2. <span data-ttu-id="69122-182">In the Backup agent, click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="69122-182">In the Backup agent, click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/schedule-backup-close.png)
3. <span data-ttu-id="69122-184">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-184">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="69122-185">On the Select Items to Backup page, click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="69122-185">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="69122-186">Select the files and folders that you want to back up, and then click **Okay**.</span><span class="sxs-lookup"><span data-stu-id="69122-186">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="69122-187">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-187">Click **Next**.</span></span>
7. <span data-ttu-id="69122-188">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-188">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="69122-189">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span><span class="sxs-lookup"><span data-stu-id="69122-189">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items for Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. <span data-ttu-id="69122-192">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span><span class="sxs-lookup"><span data-stu-id="69122-192">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="69122-193">The retention policy specifies the duration for which the backup will be stored.</span><span class="sxs-lookup"><span data-stu-id="69122-193">The retention policy specifies the duration for which the backup will be stored.</span></span> <span data-ttu-id="69122-194">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span><span class="sxs-lookup"><span data-stu-id="69122-194">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="69122-195">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="69122-195">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="69122-196">On the Choose Initial Backup Type page, choose the initial backup type.</span><span class="sxs-lookup"><span data-stu-id="69122-196">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="69122-197">Leave the option **Automatically over the network** selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="69122-197">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="69122-198">You can back up automatically over the network, or you can back up offline.</span><span class="sxs-lookup"><span data-stu-id="69122-198">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="69122-199">The remainder of this article describes the process for backing up automatically.</span><span class="sxs-lookup"><span data-stu-id="69122-199">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="69122-200">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span><span class="sxs-lookup"><span data-stu-id="69122-200">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="69122-201">On the Confirmation page, review the information, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="69122-201">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="69122-202">After the wizard finishes creating the backup schedule, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="69122-202">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling-optional"></a><span data-ttu-id="69122-203">Enable network throttling (optional)</span><span class="sxs-lookup"><span data-stu-id="69122-203">Enable network throttling (optional)</span></span>
<span data-ttu-id="69122-204">The Backup agent provides network throttling.</span><span class="sxs-lookup"><span data-stu-id="69122-204">The Backup agent provides network throttling.</span></span> <span data-ttu-id="69122-205">Throttling controls how network bandwidth is used during data transfer.</span><span class="sxs-lookup"><span data-stu-id="69122-205">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="69122-206">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="69122-206">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="69122-207">Throttling applies to back up and restore activities.</span><span class="sxs-lookup"><span data-stu-id="69122-207">Throttling applies to back up and restore activities.</span></span>

<span data-ttu-id="69122-208">**To enable network throttling**</span><span class="sxs-lookup"><span data-stu-id="69122-208">**To enable network throttling**</span></span>

1. <span data-ttu-id="69122-209">In the Backup agent, click **Change Properties**.</span><span class="sxs-lookup"><span data-stu-id="69122-209">In the Backup agent, click **Change Properties**.</span></span>

    ![Change properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/change-properties.png)
2. <span data-ttu-id="69122-211">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span><span class="sxs-lookup"><span data-stu-id="69122-211">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Network throttling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/throttling-dialog.png)
3. <span data-ttu-id="69122-213">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span><span class="sxs-lookup"><span data-stu-id="69122-213">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="69122-214">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span><span class="sxs-lookup"><span data-stu-id="69122-214">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="69122-215">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span><span class="sxs-lookup"><span data-stu-id="69122-215">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="69122-216">Hours outside of designated work hours are considered non-work hours.</span><span class="sxs-lookup"><span data-stu-id="69122-216">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="69122-217">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="69122-217">Click **OK**.</span></span>

### <a name="to-back-up-now"></a><span data-ttu-id="69122-218">To back up now</span><span class="sxs-lookup"><span data-stu-id="69122-218">To back up now</span></span>
1. <span data-ttu-id="69122-219">In the Backup agent, click **Back Up Now** to complete the initial seeding over the network.</span><span class="sxs-lookup"><span data-stu-id="69122-219">In the Backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server backup now](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/backup-now.png)
2. <span data-ttu-id="69122-221">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span><span class="sxs-lookup"><span data-stu-id="69122-221">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="69122-222">Then click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="69122-222">Then click **Back Up**.</span></span>
3. <span data-ttu-id="69122-223">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="69122-223">Click **Close** to close the wizard.</span></span> <span data-ttu-id="69122-224">If you do this before the backup process finishes, the wizard continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="69122-224">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="69122-225">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span><span class="sxs-lookup"><span data-stu-id="69122-225">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a><span data-ttu-id="69122-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="69122-227">Next steps</span></span>
* <span data-ttu-id="69122-228">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="69122-228">Sign up for a [free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="69122-229">For additional information about backing up VMs or other workloads, see:</span><span class="sxs-lookup"><span data-stu-id="69122-229">For additional information about backing up VMs or other workloads, see:</span></span>

* [<span data-ttu-id="69122-230">Back up IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="69122-230">Back up IaaS VMs</span></span>](backup-azure-vms-prepare.md)
* [<span data-ttu-id="69122-231">Back up workloads to Azure with Microsoft Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="69122-231">Back up workloads to Azure with Microsoft Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)
* [<span data-ttu-id="69122-232">Back up workloads to Azure with DPM</span><span class="sxs-lookup"><span data-stu-id="69122-232">Back up workloads to Azure with DPM</span></span>](backup-azure-dpm-introduction.md)









