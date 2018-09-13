---
title: Back up Windows system state to Azure
description: Learn to back up the system state of Windows Server and/or Windows computers to Azure.
services: backup
author: saurabhsensharma
manager: shivamg
keywords: how to backup; how to back up; backup files and folders
ms.service: backup
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: saurse
ms.openlocfilehash: 61ee1ce7d5cc6dc2aa4b7a8b02c2e5ba77539725
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869640"
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="700ad-104">Back up Windows system state in Resource Manager deployment</span><span class="sxs-lookup"><span data-stu-id="700ad-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="700ad-105">This article explains how to back up your Windows Server system state to Azure.</span><span class="sxs-lookup"><span data-stu-id="700ad-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="700ad-106">It's a tutorial intended to walk you through the basics.</span><span class="sxs-lookup"><span data-stu-id="700ad-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="700ad-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="700ad-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span><span class="sxs-lookup"><span data-stu-id="700ad-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="700ad-109">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="700ad-109">Create a recovery services vault</span></span>
<span data-ttu-id="700ad-110">To back up your Windows Server System State, you need to create a Recovery Services vault in the region where you want to store the data.</span><span class="sxs-lookup"><span data-stu-id="700ad-110">To back up your Windows Server System State, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="700ad-111">You also need to determine how you want your storage replicated.</span><span class="sxs-lookup"><span data-stu-id="700ad-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="700ad-112">To create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="700ad-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="700ad-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="700ad-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="700ad-114">On the Hub menu, click **All services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="700ad-114">On the Hub menu, click **All services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Create Recovery Services Vault step 1](./media/backup-azure-system-state/open-rs-vault-list.png) <br/>

    <span data-ttu-id="700ad-116">If there are recovery services vaults in the subscription, the vaults are listed.</span><span class="sxs-lookup"><span data-stu-id="700ad-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="700ad-117">On the **Recovery Services vaults** menu, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="700ad-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Create Recovery Services Vault step 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="700ad-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span><span class="sxs-lookup"><span data-stu-id="700ad-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Create Recovery Services Vault step 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="700ad-121">For **Name**, enter a friendly name to identify the vault.</span><span class="sxs-lookup"><span data-stu-id="700ad-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="700ad-122">The name needs to be unique for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="700ad-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="700ad-123">Type a name that contains between 2 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="700ad-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="700ad-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="700ad-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="700ad-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="700ad-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="700ad-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="700ad-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="700ad-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span><span class="sxs-lookup"><span data-stu-id="700ad-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="700ad-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="700ad-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="700ad-129">In the **Resource group** section:</span><span class="sxs-lookup"><span data-stu-id="700ad-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="700ad-130">select **Create new** if you want to create a Resource group.</span><span class="sxs-lookup"><span data-stu-id="700ad-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="700ad-131">Or</span><span class="sxs-lookup"><span data-stu-id="700ad-131">Or</span></span>
    * <span data-ttu-id="700ad-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span><span class="sxs-lookup"><span data-stu-id="700ad-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="700ad-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="700ad-134">Click **Location** to select the geographic region for the vault.</span><span class="sxs-lookup"><span data-stu-id="700ad-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="700ad-135">This choice determines the geographic region where your backup data is sent.</span><span class="sxs-lookup"><span data-stu-id="700ad-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="700ad-136">At the bottom of the Recovery Services vault blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="700ad-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="700ad-137">It can take several minutes for the Recovery Services vault to be created.</span><span class="sxs-lookup"><span data-stu-id="700ad-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="700ad-138">Monitor the status notifications in the upper right-hand area of the portal.</span><span class="sxs-lookup"><span data-stu-id="700ad-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="700ad-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="700ad-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="700ad-140">If after several minutes you don't see your vault, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="700ad-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Click Refresh button](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="700ad-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span><span class="sxs-lookup"><span data-stu-id="700ad-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="700ad-143">Set storage redundancy for the vault</span><span class="sxs-lookup"><span data-stu-id="700ad-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="700ad-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span><span class="sxs-lookup"><span data-stu-id="700ad-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="700ad-145">From the **Recovery Services vaults** blade, click the new vault.</span><span class="sxs-lookup"><span data-stu-id="700ad-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Select the new vault from the list of Recovery Services vault](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="700ad-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span><span class="sxs-lookup"><span data-stu-id="700ad-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![View the storage configuration for new vault](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="700ad-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="700ad-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="700ad-150">The Backup Infrastructure blade opens.</span><span class="sxs-lookup"><span data-stu-id="700ad-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="700ad-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="700ad-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Set the storage configuration for new vault](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="700ad-153">Choose the appropriate storage replication option for your vault.</span><span class="sxs-lookup"><span data-stu-id="700ad-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![storage configuration choices](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="700ad-155">By default, your vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="700ad-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="700ad-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span><span class="sxs-lookup"><span data-stu-id="700ad-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="700ad-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span><span class="sxs-lookup"><span data-stu-id="700ad-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="700ad-158">Read more about [geo-redundant](../storage/common/storage-redundancy-grs.md) and [locally redundant](../storage/common/storage-redundancy-lrs.md) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-158">Read more about [geo-redundant](../storage/common/storage-redundancy-grs.md) and [locally redundant](../storage/common/storage-redundancy-lrs.md) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="700ad-159">Now that you've created a vault, configure it for backing up Windows System State.</span><span class="sxs-lookup"><span data-stu-id="700ad-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="700ad-160">Configure the vault</span><span class="sxs-lookup"><span data-stu-id="700ad-160">Configure the vault</span></span>
1. <span data-ttu-id="700ad-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span><span class="sxs-lookup"><span data-stu-id="700ad-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Open backup goal blade](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="700ad-163">The **Backup Goal** blade opens.</span><span class="sxs-lookup"><span data-stu-id="700ad-163">The **Backup Goal** blade opens.</span></span>

    ![Open backup goal blade](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="700ad-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="700ad-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="700ad-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span><span class="sxs-lookup"><span data-stu-id="700ad-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="700ad-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="700ad-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configuring files and folders](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="700ad-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span><span class="sxs-lookup"><span data-stu-id="700ad-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Backup goal configured, next prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="700ad-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="700ad-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="700ad-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="700ad-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="700ad-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="700ad-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="700ad-176">In the download pop-up menu, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="700ad-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="700ad-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="700ad-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="700ad-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span><span class="sxs-lookup"><span data-stu-id="700ad-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![prepare infrastructure](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="700ad-180">You don't need to install the agent yet.</span><span class="sxs-lookup"><span data-stu-id="700ad-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="700ad-181">You can install the agent after you have downloaded the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="700ad-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="700ad-182">On the **Prepare infrastructure** blade, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="700ad-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![download vault credentials](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="700ad-184">The vault credentials download to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="700ad-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="700ad-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span><span class="sxs-lookup"><span data-stu-id="700ad-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="700ad-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="700ad-186">Click **Save**.</span></span> <span data-ttu-id="700ad-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span><span class="sxs-lookup"><span data-stu-id="700ad-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="700ad-188">You cannot open the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="700ad-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="700ad-189">Proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="700ad-189">Proceed to the next step.</span></span> <span data-ttu-id="700ad-190">The vault credentials are in the Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="700ad-190">The vault credentials are in the Downloads folder.</span></span>   

    ![vault credentials finished downloading](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)
> [!NOTE]
> <span data-ttu-id="700ad-192">The vault credentials must be saved only to a location that is local to the Windows Server on which you intend to use the agent.</span><span class="sxs-lookup"><span data-stu-id="700ad-192">The vault credentials must be saved only to a location that is local to the Windows Server on which you intend to use the agent.</span></span> 
>

[!INCLUDE [backup-upgrade-mars-agent.md](../../includes/backup-upgrade-mars-agent.md)]

## <a name="install-and-register-the-agent"></a><span data-ttu-id="700ad-193">Install and register the agent</span><span class="sxs-lookup"><span data-stu-id="700ad-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="700ad-194">Enabling backup through the Azure portal is not available, yet.</span><span class="sxs-lookup"><span data-stu-id="700ad-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="700ad-195">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span><span class="sxs-lookup"><span data-stu-id="700ad-195">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="700ad-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span><span class="sxs-lookup"><span data-stu-id="700ad-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="700ad-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="700ad-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![run Recovery Services agent installer credentials](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="700ad-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span><span class="sxs-lookup"><span data-stu-id="700ad-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="700ad-200">To complete the wizard, you need to:</span><span class="sxs-lookup"><span data-stu-id="700ad-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="700ad-201">Choose a location for the installation and cache folder.</span><span class="sxs-lookup"><span data-stu-id="700ad-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="700ad-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="700ad-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="700ad-203">Provide your user name and password details if you use an authenticated proxy.</span><span class="sxs-lookup"><span data-stu-id="700ad-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="700ad-204">Provide the downloaded vault credentials</span><span class="sxs-lookup"><span data-stu-id="700ad-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="700ad-205">Save the encryption passphrase in a secure location.</span><span class="sxs-lookup"><span data-stu-id="700ad-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="700ad-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span><span class="sxs-lookup"><span data-stu-id="700ad-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="700ad-207">Save the file in a secure location.</span><span class="sxs-lookup"><span data-stu-id="700ad-207">Save the file in a secure location.</span></span> <span data-ttu-id="700ad-208">It is required to restore a backup.</span><span class="sxs-lookup"><span data-stu-id="700ad-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="700ad-209">The agent is now installed and your machine is registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="700ad-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="700ad-210">You're ready to configure and schedule your backup.</span><span class="sxs-lookup"><span data-stu-id="700ad-210">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state"></a><span data-ttu-id="700ad-211">Back up Windows Server System State</span><span class="sxs-lookup"><span data-stu-id="700ad-211">Back up Windows Server System State</span></span> 
<span data-ttu-id="700ad-212">The initial backup includes two tasks:</span><span class="sxs-lookup"><span data-stu-id="700ad-212">The initial backup includes two tasks:</span></span>

* <span data-ttu-id="700ad-213">Schedule the backup</span><span class="sxs-lookup"><span data-stu-id="700ad-213">Schedule the backup</span></span>
* <span data-ttu-id="700ad-214">Back up  System State for the first time</span><span class="sxs-lookup"><span data-stu-id="700ad-214">Back up  System State for the first time</span></span>

<span data-ttu-id="700ad-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="700ad-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

> [!NOTE]
> <span data-ttu-id="700ad-216">You can back up System State on Windows Server 2008 R2 through Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="700ad-216">You can back up System State on Windows Server 2008 R2 through Windows Server 2016.</span></span> <span data-ttu-id="700ad-217">System State back up is not supported on client SKUs.</span><span class="sxs-lookup"><span data-stu-id="700ad-217">System State back up is not supported on client SKUs.</span></span> <span data-ttu-id="700ad-218">System State is not shown as an option for Windows clients, or Windows Server 2008 SP2 machines.</span><span class="sxs-lookup"><span data-stu-id="700ad-218">System State is not shown as an option for Windows clients, or Windows Server 2008 SP2 machines.</span></span>
>
>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="700ad-219">To schedule the backup job</span><span class="sxs-lookup"><span data-stu-id="700ad-219">To schedule the backup job</span></span>

1. <span data-ttu-id="700ad-220">Open the Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="700ad-220">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="700ad-221">You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="700ad-221">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Launch the Azure Recovery Services agent](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="700ad-223">In the Recovery Services agent, click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="700ad-223">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server back up](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="700ad-225">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="700ad-225">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="700ad-226">On the Select Items to Backup page, click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="700ad-226">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="700ad-227">Select **System State** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="700ad-227">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="700ad-228">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="700ad-228">Click **Next**.</span></span>

7. <span data-ttu-id="700ad-229">Select the required Backup frequency and the retention policy for your System State backups in the subsequent pages.</span><span class="sxs-lookup"><span data-stu-id="700ad-229">Select the required Backup frequency and the retention policy for your System State backups in the subsequent pages.</span></span> 

8. <span data-ttu-id="700ad-230">On the Confirmation page, review the information, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="700ad-230">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="700ad-231">After the wizard finishes creating the backup schedule, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="700ad-231">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="700ad-232">To back up Windows Server System State for the first time</span><span class="sxs-lookup"><span data-stu-id="700ad-232">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="700ad-233">Make sure there are no pending updates for Windows Server that require a reboot.</span><span class="sxs-lookup"><span data-stu-id="700ad-233">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="700ad-234">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span><span class="sxs-lookup"><span data-stu-id="700ad-234">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server back up now](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="700ad-236">Select **System State** on the **Select Backup Item** screen that appears and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="700ad-236">Select **System State** on the **Select Backup Item** screen that appears and click **Next**.</span></span>

4. <span data-ttu-id="700ad-237">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span><span class="sxs-lookup"><span data-stu-id="700ad-237">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="700ad-238">Then click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="700ad-238">Then click **Back Up**.</span></span>

4. <span data-ttu-id="700ad-239">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="700ad-239">Click **Close** to close the wizard.</span></span> <span data-ttu-id="700ad-240">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="700ad-240">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>


<span data-ttu-id="700ad-241">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span><span class="sxs-lookup"><span data-stu-id="700ad-241">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![IR complete](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="700ad-243">Questions?</span><span class="sxs-lookup"><span data-stu-id="700ad-243">Questions?</span></span>
<span data-ttu-id="700ad-244">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="700ad-244">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="700ad-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="700ad-245">Next steps</span></span>
* <span data-ttu-id="700ad-246">Get more details about [backing up Windows machines](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-246">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="700ad-247">Now that you've backed up your Windows Server System State, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-247">Now that you've backed up your Windows Server System State, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="700ad-248">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="700ad-248">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
