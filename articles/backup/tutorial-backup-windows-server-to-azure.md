---
title: Back up Windows Server to Azure
description: This tutorial details backing up on-premises Windows Servers to a Recovery Services vault.
services: backup
author: saurabhsensharma
manager: shivamg
keywords: windows server back up; back up windows server; back up and disaster recovery
ms.service: backup
ms.topic: tutorial
ms.date: 8/22/2018
ms.author: saurse
ms.custom: mvc
ms.openlocfilehash: 9bf4c25b416edf86d29c27bcb19901bf43073bb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855960"
---
# <a name="back-up-windows-server-to-azure"></a><span data-ttu-id="b1927-104">Back up Windows Server to Azure</span><span class="sxs-lookup"><span data-stu-id="b1927-104">Back up Windows Server to Azure</span></span>


<span data-ttu-id="b1927-105">You can use Azure Backup to protect your Windows Server from corruptions, attacks, and disasters.</span><span class="sxs-lookup"><span data-stu-id="b1927-105">You can use Azure Backup to protect your Windows Server from corruptions, attacks, and disasters.</span></span> <span data-ttu-id="b1927-106">Azure Backup provides a lightweight tool known as the Microsoft Azure Recovery Services (MARS) agent.</span><span class="sxs-lookup"><span data-stu-id="b1927-106">Azure Backup provides a lightweight tool known as the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="b1927-107">The MARS agent is installed on the Windows Server to protect files and folders, and server configuration info via Windows Server System State.</span><span class="sxs-lookup"><span data-stu-id="b1927-107">The MARS agent is installed on the Windows Server to protect files and folders, and server configuration info via Windows Server System State.</span></span> <span data-ttu-id="b1927-108">This tutorial explains how you can use MARS Agent to back up your Windows Server to Azure.</span><span class="sxs-lookup"><span data-stu-id="b1927-108">This tutorial explains how you can use MARS Agent to back up your Windows Server to Azure.</span></span> <span data-ttu-id="b1927-109">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="b1927-109">In this tutorial you learn how to:</span></span> 


> [!div class="checklist"]
> * <span data-ttu-id="b1927-110">Download and set up the MARS Agent</span><span class="sxs-lookup"><span data-stu-id="b1927-110">Download and set up the MARS Agent</span></span>
> * <span data-ttu-id="b1927-111">Configure back up times and retention schedule for your server’s backups</span><span class="sxs-lookup"><span data-stu-id="b1927-111">Configure back up times and retention schedule for your server’s backups</span></span>
> * <span data-ttu-id="b1927-112">Perform an ad-hoc back up</span><span class="sxs-lookup"><span data-stu-id="b1927-112">Perform an ad-hoc back up</span></span>


## <a name="sign-in-to-azure"></a><span data-ttu-id="b1927-113">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="b1927-113">Sign in to Azure</span></span>

<span data-ttu-id="b1927-114">Sign in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b1927-114">Sign in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b1927-115">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="b1927-115">Create a Recovery Services vault</span></span>

<span data-ttu-id="b1927-116">Before you can back up Windows Server, you must create a place for the backups, or restore points, to be stored.</span><span class="sxs-lookup"><span data-stu-id="b1927-116">Before you can back up Windows Server, you must create a place for the backups, or restore points, to be stored.</span></span> <span data-ttu-id="b1927-117">A [Recovery Services vault](backup-azure-recovery-services-vault-overview.md) is a container in Azure that stores the backups from your Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b1927-117">A [Recovery Services vault](backup-azure-recovery-services-vault-overview.md) is a container in Azure that stores the backups from your Windows Server.</span></span> <span data-ttu-id="b1927-118">Follow the steps below to create a Recovery Services vault in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b1927-118">Follow the steps below to create a Recovery Services vault in the Azure portal.</span></span> 

1. <span data-ttu-id="b1927-119">On the left-hand menu, select **All services** and in the services list, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="b1927-119">On the left-hand menu, select **All services** and in the services list, type **Recovery Services**.</span></span> <span data-ttu-id="b1927-120">Click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="b1927-120">Click **Recovery Services vaults**.</span></span>

   ![open Recovery Services vault](./media/tutorial-backup-windows-server-to-azure/full-browser-open-rs-vault_2.png)

2. <span data-ttu-id="b1927-122">On the **Recovery Services vaults** menu, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b1927-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

   ![provide information for vault](./media/tutorial-backup-windows-server-to-azure/provide-vault-detail-2.png)

3. <span data-ttu-id="b1927-124">In the **Recovery Services vault** menu,</span><span class="sxs-lookup"><span data-stu-id="b1927-124">In the **Recovery Services vault** menu,</span></span>

    - <span data-ttu-id="b1927-125">Type *myRecoveryServicesVault* in **Name**.</span><span class="sxs-lookup"><span data-stu-id="b1927-125">Type *myRecoveryServicesVault* in **Name**.</span></span>
    - <span data-ttu-id="b1927-126">The current subscription ID appears in **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="b1927-126">The current subscription ID appears in **Subscription**.</span></span>
    - <span data-ttu-id="b1927-127">For **Resource group**, select **Use existing** and choose *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b1927-127">For **Resource group**, select **Use existing** and choose *myResourceGroup*.</span></span> <span data-ttu-id="b1927-128">If *myResourceGroup* doesn't exist, select **Create New** and type *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b1927-128">If *myResourceGroup* doesn't exist, select **Create New** and type *myResourceGroup*.</span></span> 
    - <span data-ttu-id="b1927-129">From the **Location** drop-down menu, choose *West Europe*.</span><span class="sxs-lookup"><span data-stu-id="b1927-129">From the **Location** drop-down menu, choose *West Europe*.</span></span>
    - <span data-ttu-id="b1927-130">Click **Create** to create your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="b1927-130">Click **Create** to create your Recovery Services vault.</span></span>
 
<span data-ttu-id="b1927-131">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="b1927-131">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span>

## <a name="download-recovery-services-agent"></a><span data-ttu-id="b1927-132">Download Recovery Services agent</span><span class="sxs-lookup"><span data-stu-id="b1927-132">Download Recovery Services agent</span></span>

<span data-ttu-id="b1927-133">The Microsoft Azure Recovery Services (MARS) agent creates an association between Windows Server and your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="b1927-133">The Microsoft Azure Recovery Services (MARS) agent creates an association between Windows Server and your Recovery Services vault.</span></span> <span data-ttu-id="b1927-134">The following procedure explains how to download the agent to your server.</span><span class="sxs-lookup"><span data-stu-id="b1927-134">The following procedure explains how to download the agent to your server.</span></span>

1. <span data-ttu-id="b1927-135">From the list of Recovery Services vaults, select **myRecoveryServicesVault** to open its dashboard.</span><span class="sxs-lookup"><span data-stu-id="b1927-135">From the list of Recovery Services vaults, select **myRecoveryServicesVault** to open its dashboard.</span></span>

   ![provide information for vault](./media/tutorial-backup-windows-server-to-azure/open-vault-from-list.png)

2. <span data-ttu-id="b1927-137">On the vault dashboard menu, click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b1927-137">On the vault dashboard menu, click **Backup**.</span></span>

3. <span data-ttu-id="b1927-138">On the **Backup Goal** menu:</span><span class="sxs-lookup"><span data-stu-id="b1927-138">On the **Backup Goal** menu:</span></span>

   * <span data-ttu-id="b1927-139">for **Where is your workload running?**, select **On-premises**,</span><span class="sxs-lookup"><span data-stu-id="b1927-139">for **Where is your workload running?**, select **On-premises**,</span></span> 
   * <span data-ttu-id="b1927-140">for **What do you want to backup?**, select **Files and folders** and **System State**</span><span class="sxs-lookup"><span data-stu-id="b1927-140">for **What do you want to backup?**, select **Files and folders** and **System State**</span></span>

   ![provide information for vault](./media/tutorial-backup-windows-server-to-azure/backup-goal.png)

4. <span data-ttu-id="b1927-142">Click **Prepare Infrastructure** to open the **Prepare infrastructure** menu.</span><span class="sxs-lookup"><span data-stu-id="b1927-142">Click **Prepare Infrastructure** to open the **Prepare infrastructure** menu.</span></span>

5. <span data-ttu-id="b1927-143">On the **Prepare infrastructure** menu, click **Download Agent for Windows Server or Windows Client** to download the *MARSAgentInstaller.exe*.</span><span class="sxs-lookup"><span data-stu-id="b1927-143">On the **Prepare infrastructure** menu, click **Download Agent for Windows Server or Windows Client** to download the *MARSAgentInstaller.exe*.</span></span> 

    ![prepare infrastructure](./media/tutorial-backup-windows-server-to-azure/prepare-infrastructure.png)

    <span data-ttu-id="b1927-145">The installer opens a separate browser and downloads **MARSAgentInstaller.exe**.</span><span class="sxs-lookup"><span data-stu-id="b1927-145">The installer opens a separate browser and downloads **MARSAgentInstaller.exe**.</span></span>
 
6. <span data-ttu-id="b1927-146">Before you run the downloaded file, on the Prepare infrastructure menu click **Download** and save the **Vault Credentials** file.</span><span class="sxs-lookup"><span data-stu-id="b1927-146">Before you run the downloaded file, on the Prepare infrastructure menu click **Download** and save the **Vault Credentials** file.</span></span> <span data-ttu-id="b1927-147">Vault credentials are required to connect the MARS Agent with the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="b1927-147">Vault credentials are required to connect the MARS Agent with the Recovery Services vault.</span></span>

    ![prepare infrastructure](./media/tutorial-backup-windows-server-to-azure/download-vault-credentials.png)
 
## <a name="install-and-register-the-agent"></a><span data-ttu-id="b1927-149">Install and register the agent</span><span class="sxs-lookup"><span data-stu-id="b1927-149">Install and register the agent</span></span>

1. <span data-ttu-id="b1927-150">Locate and double-click the downloaded **MARSagentinstaller.exe**.</span><span class="sxs-lookup"><span data-stu-id="b1927-150">Locate and double-click the downloaded **MARSagentinstaller.exe**.</span></span>
2. <span data-ttu-id="b1927-151">The **Microsoft Azure Recovery Services Agent Setup Wizard** appears.</span><span class="sxs-lookup"><span data-stu-id="b1927-151">The **Microsoft Azure Recovery Services Agent Setup Wizard** appears.</span></span> <span data-ttu-id="b1927-152">As you go through the wizard, provide the following information when prompted and click **Register**.</span><span class="sxs-lookup"><span data-stu-id="b1927-152">As you go through the wizard, provide the following information when prompted and click **Register**.</span></span>
    - <span data-ttu-id="b1927-153">Location for the installation and cache folder.</span><span class="sxs-lookup"><span data-stu-id="b1927-153">Location for the installation and cache folder.</span></span>
    - <span data-ttu-id="b1927-154">Proxy server info if you use a proxy server to connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="b1927-154">Proxy server info if you use a proxy server to connect to the internet.</span></span>
    - <span data-ttu-id="b1927-155">Your user name and password details if you use an authenticated proxy.</span><span class="sxs-lookup"><span data-stu-id="b1927-155">Your user name and password details if you use an authenticated proxy.</span></span>

    ![prepare infrastructure](./media/tutorial-backup-windows-server-to-azure/mars-installer.png) 

3. <span data-ttu-id="b1927-157">At the end of the wizard, click **Proceed to Registration** and provide the **Vault Credentials** file you downloaded in the previous procedure.</span><span class="sxs-lookup"><span data-stu-id="b1927-157">At the end of the wizard, click **Proceed to Registration** and provide the **Vault Credentials** file you downloaded in the previous procedure.</span></span>
 
4. <span data-ttu-id="b1927-158">When prompted, provide an encryption passphrase to encrypt backups from Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b1927-158">When prompted, provide an encryption passphrase to encrypt backups from Windows Server.</span></span> <span data-ttu-id="b1927-159">Save the passphrase in a secure location as Microsoft cannot recover the passphrase if it is lost.</span><span class="sxs-lookup"><span data-stu-id="b1927-159">Save the passphrase in a secure location as Microsoft cannot recover the passphrase if it is lost.</span></span>

5. <span data-ttu-id="b1927-160">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b1927-160">Click **Finish**.</span></span> 

## <a name="configure-backup-and-retention"></a><span data-ttu-id="b1927-161">Configure Backup and Retention</span><span class="sxs-lookup"><span data-stu-id="b1927-161">Configure Backup and Retention</span></span>

<span data-ttu-id="b1927-162">You use the Microsoft Azure Recovery Services agent to schedule when backups to Azure, occur on Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b1927-162">You use the Microsoft Azure Recovery Services agent to schedule when backups to Azure, occur on Windows Server.</span></span> <span data-ttu-id="b1927-163">Execute the following steps on the server where you downloaded the agent.</span><span class="sxs-lookup"><span data-stu-id="b1927-163">Execute the following steps on the server where you downloaded the agent.</span></span>

1. <span data-ttu-id="b1927-164">Open the Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="b1927-164">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="b1927-165">You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="b1927-165">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

2.  <span data-ttu-id="b1927-166">In the Recovery Services agent console, click **Schedule Backup** under the **Actions Pane**.</span><span class="sxs-lookup"><span data-stu-id="b1927-166">In the Recovery Services agent console, click **Schedule Backup** under the **Actions Pane**.</span></span>

    ![prepare infrastructure](./media/tutorial-backup-windows-server-to-azure/mars-schedule-backup.png)

3. <span data-ttu-id="b1927-168">Click **Next** to navigate to the **Select Items to Back up** page.</span><span class="sxs-lookup"><span data-stu-id="b1927-168">Click **Next** to navigate to the **Select Items to Back up** page.</span></span>

4. <span data-ttu-id="b1927-169">Click **Add Items** and from the dialog box that opens, select **System State** and files or folders that you want to back up.</span><span class="sxs-lookup"><span data-stu-id="b1927-169">Click **Add Items** and from the dialog box that opens, select **System State** and files or folders that you want to back up.</span></span> <span data-ttu-id="b1927-170">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1927-170">Then click **OK**.</span></span>

5. <span data-ttu-id="b1927-171">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1927-171">Click **Next**.</span></span>

6. <span data-ttu-id="b1927-172">On the **Specify Backup Schedule (System State)** page, specify the time of the day, or week when backups need to be triggered for System State and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1927-172">On the **Specify Backup Schedule (System State)** page, specify the time of the day, or week when backups need to be triggered for System State and click **Next**.</span></span>

7. <span data-ttu-id="b1927-173">On the **Select Retention Policy (System State)** page, select the Retention Policy for the backup copy for System State and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1927-173">On the **Select Retention Policy (System State)** page, select the Retention Policy for the backup copy for System State and click **Next**.</span></span>

8. <span data-ttu-id="b1927-174">Similarly, select the backup schedule and retention policy for selected files and folders.</span><span class="sxs-lookup"><span data-stu-id="b1927-174">Similarly, select the backup schedule and retention policy for selected files and folders.</span></span> 

9. <span data-ttu-id="b1927-175">On the **Choose Initial Back up Type** page, select **Automatically over the network**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1927-175">On the **Choose Initial Back up Type** page, select **Automatically over the network**, and click **Next**.</span></span>

10. <span data-ttu-id="b1927-176">On the **Confirmation** page, review the information, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b1927-176">On the **Confirmation** page, review the information, and click **Finish**.</span></span>

11. <span data-ttu-id="b1927-177">After the wizard finishes creating the backup schedule, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="b1927-177">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

## <a name="perform-an-ad-hoc-back-up"></a><span data-ttu-id="b1927-178">Perform an ad-hoc back up</span><span class="sxs-lookup"><span data-stu-id="b1927-178">Perform an ad-hoc back up</span></span>

<span data-ttu-id="b1927-179">You have established the schedule when backup jobs run.</span><span class="sxs-lookup"><span data-stu-id="b1927-179">You have established the schedule when backup jobs run.</span></span> <span data-ttu-id="b1927-180">However, you have not backed up the server.</span><span class="sxs-lookup"><span data-stu-id="b1927-180">However, you have not backed up the server.</span></span> <span data-ttu-id="b1927-181">It is a disaster recovery best practice to run an on-demand backup to ensure data resiliency for your server.</span><span class="sxs-lookup"><span data-stu-id="b1927-181">It is a disaster recovery best practice to run an on-demand backup to ensure data resiliency for your server.</span></span>

1.  <span data-ttu-id="b1927-182">In the Microsoft Azure Recovery Services agent console, click **Back Up Now**.</span><span class="sxs-lookup"><span data-stu-id="b1927-182">In the Microsoft Azure Recovery Services agent console, click **Back Up Now**.</span></span>

    ![prepare infrastructure](./media/tutorial-backup-windows-server-to-azure/backup-now.png)

2.  <span data-ttu-id="b1927-184">On the **Back Up Now** wizard, select one from **Files and Folders** or **System State** that you want to back up and click **Next**</span><span class="sxs-lookup"><span data-stu-id="b1927-184">On the **Back Up Now** wizard, select one from **Files and Folders** or **System State** that you want to back up and click **Next**</span></span> 
3. <span data-ttu-id="b1927-185">On the **Confirmation** page, review the settings that the **Back Up Now** wizard uses to back up your server.</span><span class="sxs-lookup"><span data-stu-id="b1927-185">On the **Confirmation** page, review the settings that the **Back Up Now** wizard uses to back up your server.</span></span> <span data-ttu-id="b1927-186">Then click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="b1927-186">Then click **Back Up**.</span></span>
4.  <span data-ttu-id="b1927-187">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="b1927-187">Click **Close** to close the wizard.</span></span> <span data-ttu-id="b1927-188">If you close the wizard before the back up process finishes, the wizard continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="b1927-188">If you close the wizard before the back up process finishes, the wizard continues to run in the background.</span></span>
4.  <span data-ttu-id="b1927-189">After the initial backup is completed, **Job completed** status appears in **Jobs** pane of the MARS agent console.</span><span class="sxs-lookup"><span data-stu-id="b1927-189">After the initial backup is completed, **Job completed** status appears in **Jobs** pane of the MARS agent console.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b1927-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1927-190">Next steps</span></span>

<span data-ttu-id="b1927-191">In this tutorial, you used the Azure portal to:</span><span class="sxs-lookup"><span data-stu-id="b1927-191">In this tutorial, you used the Azure portal to:</span></span> 
 
> [!div class="checklist"] 
> * <span data-ttu-id="b1927-192">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="b1927-192">Create a Recovery Services vault</span></span> 
> * <span data-ttu-id="b1927-193">Download the Microsoft Azure Recovery Services agent</span><span class="sxs-lookup"><span data-stu-id="b1927-193">Download the Microsoft Azure Recovery Services agent</span></span> 
> * <span data-ttu-id="b1927-194">Install the agent</span><span class="sxs-lookup"><span data-stu-id="b1927-194">Install the agent</span></span> 
> * <span data-ttu-id="b1927-195">Configure backup for Windows Server</span><span class="sxs-lookup"><span data-stu-id="b1927-195">Configure backup for Windows Server</span></span> 
> * <span data-ttu-id="b1927-196">Perform an on-demand backup</span><span class="sxs-lookup"><span data-stu-id="b1927-196">Perform an on-demand backup</span></span> 

<span data-ttu-id="b1927-197">Continue to the next tutorial to recover files from Azure to Windows Server</span><span class="sxs-lookup"><span data-stu-id="b1927-197">Continue to the next tutorial to recover files from Azure to Windows Server</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="b1927-198">Restore files from Azure to Windows Server</span><span class="sxs-lookup"><span data-stu-id="b1927-198">Restore files from Azure to Windows Server</span></span>](./tutorial-backup-restore-files-windows-server.md) 

