---
title: Use Azure Backup agent to back up files and folders | Microsoft Docs
description: Use the Microsoft Azure Backup agent to back up Windows files and folders to Azure. Create a Recovery Services vault, install the Backup agent, define the backup policy, and run the initial backup on the files and folders.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: backup vault; back up a Windows server; backup windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/23/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 41bfa94b0ded7c6d74153d14ecd862874ad8a097
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670729"
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="083b8-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="083b8-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](backup-configure-vault.md)
> * [Classic portal](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="083b8-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="083b8-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Backup process steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="083b8-110">Before you start</span><span class="sxs-lookup"><span data-stu-id="083b8-110">Before you start</span></span>
<span data-ttu-id="083b8-111">To back up a server or client to Azure, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="083b8-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="083b8-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="083b8-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="083b8-113">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="083b8-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="083b8-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span><span class="sxs-lookup"><span data-stu-id="083b8-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="083b8-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span><span class="sxs-lookup"><span data-stu-id="083b8-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="083b8-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span><span class="sxs-lookup"><span data-stu-id="083b8-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="083b8-117">To create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="083b8-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="083b8-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="083b8-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="083b8-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="083b8-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="083b8-121">If there are recovery services vaults in the subscription, the vaults are listed.</span><span class="sxs-lookup"><span data-stu-id="083b8-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="083b8-122">On the **Recovery Services vaults** menu, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="083b8-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Create Recovery Services Vault step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="083b8-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span><span class="sxs-lookup"><span data-stu-id="083b8-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Create Recovery Services Vault step 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="083b8-126">For **Name**, enter a friendly name to identify the vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="083b8-127">The name needs to be unique for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="083b8-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="083b8-128">Type a name that contains between 2 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="083b8-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="083b8-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="083b8-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="083b8-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="083b8-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="083b8-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="083b8-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="083b8-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span><span class="sxs-lookup"><span data-stu-id="083b8-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="083b8-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="083b8-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="083b8-134">In the **Resource group** section:</span><span class="sxs-lookup"><span data-stu-id="083b8-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="083b8-135">select **Create new** if you want to create a new Resource group.</span><span class="sxs-lookup"><span data-stu-id="083b8-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="083b8-136">Or</span><span class="sxs-lookup"><span data-stu-id="083b8-136">Or</span></span>
    * <span data-ttu-id="083b8-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span><span class="sxs-lookup"><span data-stu-id="083b8-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="083b8-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="083b8-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="083b8-139">Click **Location** to select the geographic region for the vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="083b8-140">This choice determines the geographic region where your backup data is sent.</span><span class="sxs-lookup"><span data-stu-id="083b8-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="083b8-141">At the bottom of the Recovery Services vault blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="083b8-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="083b8-142">It can take several minutes for the Recovery Services vault to be created.</span><span class="sxs-lookup"><span data-stu-id="083b8-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="083b8-143">Monitor the status notifications in the upper right-hand area of the portal.</span><span class="sxs-lookup"><span data-stu-id="083b8-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="083b8-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="083b8-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="083b8-145">If after several minutes you don't see your vault, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="083b8-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Click Refresh button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="083b8-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span><span class="sxs-lookup"><span data-stu-id="083b8-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="083b8-148">Set storage redundancy</span><span class="sxs-lookup"><span data-stu-id="083b8-148">Set storage redundancy</span></span>
<span data-ttu-id="083b8-149">When you first create a Recovery Services vault you determine how storage is replicated.</span><span class="sxs-lookup"><span data-stu-id="083b8-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="083b8-150">From the **Recovery Services vaults** blade, click the new vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Select the new vault from the list of Recovery Services vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="083b8-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span><span class="sxs-lookup"><span data-stu-id="083b8-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![View the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="083b8-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="083b8-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="083b8-155">The Backup Infrastructure blade opens.</span><span class="sxs-lookup"><span data-stu-id="083b8-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="083b8-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="083b8-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Set the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="083b8-158">Choose the appropriate storage replication option for your vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![storage configuration choices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="083b8-160">By default, your vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="083b8-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="083b8-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span><span class="sxs-lookup"><span data-stu-id="083b8-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="083b8-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span><span class="sxs-lookup"><span data-stu-id="083b8-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="083b8-163">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="083b8-163">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span></span>

<span data-ttu-id="083b8-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="083b8-165">Configure the vault</span><span class="sxs-lookup"><span data-stu-id="083b8-165">Configure the vault</span></span>

1. <span data-ttu-id="083b8-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span><span class="sxs-lookup"><span data-stu-id="083b8-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Open backup goal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="083b8-168">The **Backup Goal** blade opens.</span><span class="sxs-lookup"><span data-stu-id="083b8-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="083b8-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span><span class="sxs-lookup"><span data-stu-id="083b8-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Open backup goal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="083b8-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="083b8-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="083b8-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span><span class="sxs-lookup"><span data-stu-id="083b8-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="083b8-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="083b8-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuring files and folders](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="083b8-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span><span class="sxs-lookup"><span data-stu-id="083b8-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Backup goal configured, next prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="083b8-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="083b8-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="083b8-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="083b8-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="083b8-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="083b8-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="083b8-182">In the download pop-up menu, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="083b8-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="083b8-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="083b8-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="083b8-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span><span class="sxs-lookup"><span data-stu-id="083b8-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="083b8-186">You don't need to install the agent yet.</span><span class="sxs-lookup"><span data-stu-id="083b8-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="083b8-187">You can install the agent after you have downloaded the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="083b8-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="083b8-188">On the **Prepare infrastructure** blade, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="083b8-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![download vault credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="083b8-190">The vault credentials download to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="083b8-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="083b8-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span><span class="sxs-lookup"><span data-stu-id="083b8-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="083b8-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="083b8-192">Click **Save**.</span></span> <span data-ttu-id="083b8-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span><span class="sxs-lookup"><span data-stu-id="083b8-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="083b8-194">You cannot open the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="083b8-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="083b8-195">Proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="083b8-195">Proceed to the next step.</span></span> <span data-ttu-id="083b8-196">The vault credentials are in the Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="083b8-196">The vault credentials are in the Downloads folder.</span></span>   

  ![vault credentials finished downloading](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="083b8-198">Install and register the agent</span><span class="sxs-lookup"><span data-stu-id="083b8-198">Install and register the agent</span></span>

> [!NOTE]
> Enabling backup through the Azure portal is not available, yet. Use the Microsoft Azure Recovery Services Agent to back up your files and folders.
>

1. <span data-ttu-id="083b8-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span><span class="sxs-lookup"><span data-stu-id="083b8-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="083b8-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="083b8-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![run Recovery Services agent installer credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="083b8-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span><span class="sxs-lookup"><span data-stu-id="083b8-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="083b8-205">To complete the wizard, you need to:</span><span class="sxs-lookup"><span data-stu-id="083b8-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="083b8-206">Choose a location for the installation and cache folder.</span><span class="sxs-lookup"><span data-stu-id="083b8-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="083b8-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="083b8-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="083b8-208">Provide your user name and password details if you use an authenticated proxy.</span><span class="sxs-lookup"><span data-stu-id="083b8-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="083b8-209">Provide the downloaded vault credentials</span><span class="sxs-lookup"><span data-stu-id="083b8-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="083b8-210">Save the encryption passphrase in a secure location.</span><span class="sxs-lookup"><span data-stu-id="083b8-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > If you lose or forget the passphrase, Microsoft cannot help recover the backup data. Save the file in a secure location. It is required to restore a backup.
  >
  >

<span data-ttu-id="083b8-214">The agent is now installed and your machine is registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="083b8-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="083b8-215">You're ready to configure and schedule your backup.</span><span class="sxs-lookup"><span data-stu-id="083b8-215">You're ready to configure and schedule your backup.</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="083b8-216">Create the backup policy</span><span class="sxs-lookup"><span data-stu-id="083b8-216">Create the backup policy</span></span>
<span data-ttu-id="083b8-217">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span><span class="sxs-lookup"><span data-stu-id="083b8-217">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="083b8-218">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span><span class="sxs-lookup"><span data-stu-id="083b8-218">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="083b8-219">To create a backup schedule</span><span class="sxs-lookup"><span data-stu-id="083b8-219">To create a backup schedule</span></span>
1. <span data-ttu-id="083b8-220">Open the Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="083b8-220">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="083b8-221">You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="083b8-221">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Launch the Azure Backup agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="083b8-223">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span><span class="sxs-lookup"><span data-stu-id="083b8-223">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Schedule a Windows Server backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="083b8-225">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="083b8-225">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="083b8-226">On the **Select Items to Backup** page, click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="083b8-226">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="083b8-227">The Select Items dialog opens.</span><span class="sxs-lookup"><span data-stu-id="083b8-227">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="083b8-228">Select the files and folders that you want to protect, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="083b8-228">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="083b8-229">In the **Select Items to Backup** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="083b8-229">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="083b8-230">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="083b8-230">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="083b8-231">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span><span class="sxs-lookup"><span data-stu-id="083b8-231">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items for Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. <span data-ttu-id="083b8-234">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="083b8-234">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="083b8-235">The retention policy specifies the duration which the backup is stored.</span><span class="sxs-lookup"><span data-stu-id="083b8-235">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="083b8-236">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span><span class="sxs-lookup"><span data-stu-id="083b8-236">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="083b8-237">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="083b8-237">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="083b8-238">On the Choose Initial Backup Type page, choose the initial backup type.</span><span class="sxs-lookup"><span data-stu-id="083b8-238">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="083b8-239">Leave the option **Automatically over the network** selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="083b8-239">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="083b8-240">You can back up automatically over the network, or you can back up offline.</span><span class="sxs-lookup"><span data-stu-id="083b8-240">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="083b8-241">The remainder of this article describes the process for backing up automatically.</span><span class="sxs-lookup"><span data-stu-id="083b8-241">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="083b8-242">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span><span class="sxs-lookup"><span data-stu-id="083b8-242">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="083b8-243">On the Confirmation page, review the information, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="083b8-243">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="083b8-244">After the wizard finishes creating the backup schedule, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="083b8-244">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="083b8-245">Enable network throttling</span><span class="sxs-lookup"><span data-stu-id="083b8-245">Enable network throttling</span></span>
<span data-ttu-id="083b8-246">The Microsoft Azure Backup agent provides network throttling.</span><span class="sxs-lookup"><span data-stu-id="083b8-246">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="083b8-247">Throttling controls how network bandwidth is used during data transfer.</span><span class="sxs-lookup"><span data-stu-id="083b8-247">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="083b8-248">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="083b8-248">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="083b8-249">Throttling applies to back up and restore activities.</span><span class="sxs-lookup"><span data-stu-id="083b8-249">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs). The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system. Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling. Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).
>
>

<span data-ttu-id="083b8-254">**To enable network throttling**</span><span class="sxs-lookup"><span data-stu-id="083b8-254">**To enable network throttling**</span></span>

1. <span data-ttu-id="083b8-255">In the Microsoft Azure Backup agent, click **Change Properties**.</span><span class="sxs-lookup"><span data-stu-id="083b8-255">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Change properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="083b8-257">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span><span class="sxs-lookup"><span data-stu-id="083b8-257">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Network throttling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="083b8-259">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span><span class="sxs-lookup"><span data-stu-id="083b8-259">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="083b8-260">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span><span class="sxs-lookup"><span data-stu-id="083b8-260">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="083b8-261">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span><span class="sxs-lookup"><span data-stu-id="083b8-261">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="083b8-262">Hours outside of designated work hours are considered non-work hours.</span><span class="sxs-lookup"><span data-stu-id="083b8-262">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="083b8-263">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="083b8-263">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="083b8-264">To back up files and folders for the first time</span><span class="sxs-lookup"><span data-stu-id="083b8-264">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="083b8-265">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span><span class="sxs-lookup"><span data-stu-id="083b8-265">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server backup now](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="083b8-267">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span><span class="sxs-lookup"><span data-stu-id="083b8-267">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="083b8-268">Then click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="083b8-268">Then click **Back Up**.</span></span>
3. <span data-ttu-id="083b8-269">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="083b8-269">Click **Close** to close the wizard.</span></span> <span data-ttu-id="083b8-270">If you do this before the backup process finishes, the wizard continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="083b8-270">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="083b8-271">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span><span class="sxs-lookup"><span data-stu-id="083b8-271">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="083b8-273">Questions?</span><span class="sxs-lookup"><span data-stu-id="083b8-273">Questions?</span></span>
<span data-ttu-id="083b8-274">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="083b8-274">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="083b8-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="083b8-275">Next steps</span></span>
<span data-ttu-id="083b8-276">For additional information about backing up VMs or other workloads, see:</span><span class="sxs-lookup"><span data-stu-id="083b8-276">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="083b8-277">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="083b8-277">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="083b8-278">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="083b8-278">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>


























