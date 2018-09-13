---
title: Back up Windows files and folders to Azure (Resource Manager) | Microsoft Docs
description: Learn to back up Windows files and folders to Azure in a Resource Manager deployment.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: how to backup; how to back up; backup files and folders
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 2/23/2017
ms.author: markgal;
ms.openlocfilehash: 1f980793f989796c604f49fa74824af5aa26b304
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554036"
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="f59d1-104">First look: back up files and folders in Resource Manager deployment</span><span class="sxs-lookup"><span data-stu-id="f59d1-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="f59d1-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span><span class="sxs-lookup"><span data-stu-id="f59d1-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="f59d1-106">It's a tutorial intended to walk you through the basics.</span><span class="sxs-lookup"><span data-stu-id="f59d1-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="f59d1-107">If you want to get started using Azure Backup, you're in the right place.</span><span class="sxs-lookup"><span data-stu-id="f59d1-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="f59d1-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="f59d1-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span><span class="sxs-lookup"><span data-stu-id="f59d1-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f59d1-110">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="f59d1-110">Create a recovery services vault</span></span>
<span data-ttu-id="f59d1-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span><span class="sxs-lookup"><span data-stu-id="f59d1-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="f59d1-112">You also need to determine how you want your storage replicated.</span><span class="sxs-lookup"><span data-stu-id="f59d1-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="f59d1-113">To create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="f59d1-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="f59d1-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f59d1-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="f59d1-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="f59d1-117">If there are recovery services vaults in the subscription, the vaults are listed.</span><span class="sxs-lookup"><span data-stu-id="f59d1-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="f59d1-118">On the **Recovery Services vaults** menu, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Create Recovery Services Vault step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="f59d1-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Create Recovery Services Vault step 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="f59d1-122">For **Name**, enter a friendly name to identify the vault.</span><span class="sxs-lookup"><span data-stu-id="f59d1-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="f59d1-123">The name needs to be unique for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f59d1-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="f59d1-124">Type a name that contains between 2 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="f59d1-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="f59d1-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="f59d1-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="f59d1-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f59d1-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="f59d1-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="f59d1-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="f59d1-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span><span class="sxs-lookup"><span data-stu-id="f59d1-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="f59d1-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f59d1-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="f59d1-130">In the **Resource group** section:</span><span class="sxs-lookup"><span data-stu-id="f59d1-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="f59d1-131">select **Create new** if you want to create a new Resource group.</span><span class="sxs-lookup"><span data-stu-id="f59d1-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="f59d1-132">Or</span><span class="sxs-lookup"><span data-stu-id="f59d1-132">Or</span></span>
    * <span data-ttu-id="f59d1-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span><span class="sxs-lookup"><span data-stu-id="f59d1-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="f59d1-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="f59d1-135">Click **Location** to select the geographic region for the vault.</span><span class="sxs-lookup"><span data-stu-id="f59d1-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="f59d1-136">This choice determines the geographic region where your backup data is sent.</span><span class="sxs-lookup"><span data-stu-id="f59d1-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="f59d1-137">At the bottom of the Recovery Services vault blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="f59d1-138">It can take several minutes for the Recovery Services vault to be created.</span><span class="sxs-lookup"><span data-stu-id="f59d1-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="f59d1-139">Monitor the status notifications in the upper right-hand area of the portal.</span><span class="sxs-lookup"><span data-stu-id="f59d1-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="f59d1-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="f59d1-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="f59d1-141">If after several minutes you don't see your vault, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Click Refresh button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="f59d1-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span><span class="sxs-lookup"><span data-stu-id="f59d1-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="f59d1-144">Set storage redundancy for the vault</span><span class="sxs-lookup"><span data-stu-id="f59d1-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="f59d1-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span><span class="sxs-lookup"><span data-stu-id="f59d1-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="f59d1-146">From the **Recovery Services vaults** blade, click the new vault.</span><span class="sxs-lookup"><span data-stu-id="f59d1-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Select the new vault from the list of Recovery Services vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="f59d1-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span><span class="sxs-lookup"><span data-stu-id="f59d1-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![View the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="f59d1-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="f59d1-151">The Backup Infrastructure blade opens.</span><span class="sxs-lookup"><span data-stu-id="f59d1-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="f59d1-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="f59d1-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Set the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="f59d1-154">Choose the appropriate storage replication option for your vault.</span><span class="sxs-lookup"><span data-stu-id="f59d1-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![storage configuration choices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="f59d1-156">By default, your vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="f59d1-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="f59d1-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="f59d1-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span><span class="sxs-lookup"><span data-stu-id="f59d1-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="f59d1-159">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-159">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span></span>

<span data-ttu-id="f59d1-160">Now that you've created a vault, configure it for backing up files and folders.</span><span class="sxs-lookup"><span data-stu-id="f59d1-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="f59d1-161">Configure the vault</span><span class="sxs-lookup"><span data-stu-id="f59d1-161">Configure the vault</span></span>
1. <span data-ttu-id="f59d1-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Open backup goal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="f59d1-164">The **Backup Goal** blade opens.</span><span class="sxs-lookup"><span data-stu-id="f59d1-164">The **Backup Goal** blade opens.</span></span>

    ![Open backup goal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="f59d1-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="f59d1-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span><span class="sxs-lookup"><span data-stu-id="f59d1-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="f59d1-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configuring files and folders](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="f59d1-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span><span class="sxs-lookup"><span data-stu-id="f59d1-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Backup goal configured, next prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="f59d1-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="f59d1-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="f59d1-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="f59d1-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="f59d1-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="f59d1-177">In the download pop-up menu, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="f59d1-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="f59d1-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="f59d1-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span><span class="sxs-lookup"><span data-stu-id="f59d1-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![prepare infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="f59d1-181">You don't need to install the agent yet.</span><span class="sxs-lookup"><span data-stu-id="f59d1-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="f59d1-182">You can install the agent after you have downloaded the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="f59d1-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="f59d1-183">On the **Prepare infrastructure** blade, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![download vault credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="f59d1-185">The vault credentials download to your Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="f59d1-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="f59d1-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span><span class="sxs-lookup"><span data-stu-id="f59d1-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="f59d1-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-187">Click **Save**.</span></span> <span data-ttu-id="f59d1-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span><span class="sxs-lookup"><span data-stu-id="f59d1-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="f59d1-189">You cannot open the vault credentials.</span><span class="sxs-lookup"><span data-stu-id="f59d1-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="f59d1-190">Proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="f59d1-190">Proceed to the next step.</span></span> <span data-ttu-id="f59d1-191">The vault credentials are in the Downloads folder.</span><span class="sxs-lookup"><span data-stu-id="f59d1-191">The vault credentials are in the Downloads folder.</span></span>   

    ![vault credentials finished downloading](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="f59d1-193">Install and register the agent</span><span class="sxs-lookup"><span data-stu-id="f59d1-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="f59d1-194">Enabling backup through the Azure portal is not available, yet.</span><span class="sxs-lookup"><span data-stu-id="f59d1-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="f59d1-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span><span class="sxs-lookup"><span data-stu-id="f59d1-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="f59d1-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span><span class="sxs-lookup"><span data-stu-id="f59d1-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="f59d1-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="f59d1-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![run Recovery Services agent installer credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="f59d1-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span><span class="sxs-lookup"><span data-stu-id="f59d1-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="f59d1-200">To complete the wizard, you need to:</span><span class="sxs-lookup"><span data-stu-id="f59d1-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="f59d1-201">Choose a location for the installation and cache folder.</span><span class="sxs-lookup"><span data-stu-id="f59d1-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="f59d1-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="f59d1-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="f59d1-203">Provide your user name and password details if you use an authenticated proxy.</span><span class="sxs-lookup"><span data-stu-id="f59d1-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="f59d1-204">Provide the downloaded vault credentials</span><span class="sxs-lookup"><span data-stu-id="f59d1-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="f59d1-205">Save the encryption passphrase in a secure location.</span><span class="sxs-lookup"><span data-stu-id="f59d1-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f59d1-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span><span class="sxs-lookup"><span data-stu-id="f59d1-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="f59d1-207">Save the file in a secure location.</span><span class="sxs-lookup"><span data-stu-id="f59d1-207">Save the file in a secure location.</span></span> <span data-ttu-id="f59d1-208">It is required to restore a backup.</span><span class="sxs-lookup"><span data-stu-id="f59d1-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="f59d1-209">The agent is now installed and your machine is registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="f59d1-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="f59d1-210">You're ready to configure and schedule your backup.</span><span class="sxs-lookup"><span data-stu-id="f59d1-210">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="f59d1-211">Back up your files and folders</span><span class="sxs-lookup"><span data-stu-id="f59d1-211">Back up your files and folders</span></span>
<span data-ttu-id="f59d1-212">The initial backup includes two key tasks:</span><span class="sxs-lookup"><span data-stu-id="f59d1-212">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="f59d1-213">Schedule the backup</span><span class="sxs-lookup"><span data-stu-id="f59d1-213">Schedule the backup</span></span>
* <span data-ttu-id="f59d1-214">Back up files and folders for the first time</span><span class="sxs-lookup"><span data-stu-id="f59d1-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="f59d1-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="f59d1-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="f59d1-216">To schedule the backup job</span><span class="sxs-lookup"><span data-stu-id="f59d1-216">To schedule the backup job</span></span>
1. <span data-ttu-id="f59d1-217">Open the Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="f59d1-217">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="f59d1-218">You can find it by searching your machine for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-218">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Launch the Azure Recovery Services agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="f59d1-220">In the Recovery Services agent, click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-220">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server back up](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="f59d1-222">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-222">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="f59d1-223">On the Select Items to Backup page, click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-223">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="f59d1-224">Select the files and folders that you want to back up, and then click **Okay**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-224">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="f59d1-225">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-225">Click **Next**.</span></span>
7. <span data-ttu-id="f59d1-226">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-226">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="f59d1-227">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span><span class="sxs-lookup"><span data-stu-id="f59d1-227">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items for Windows Server Back up](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="f59d1-229">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-229">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="f59d1-230">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span><span class="sxs-lookup"><span data-stu-id="f59d1-230">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="f59d1-231">The retention policy specifies how long the backup data is stored.</span><span class="sxs-lookup"><span data-stu-id="f59d1-231">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="f59d1-232">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span><span class="sxs-lookup"><span data-stu-id="f59d1-232">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="f59d1-233">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="f59d1-233">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="f59d1-234">On the Choose Initial Backup Type page, choose the initial backup type.</span><span class="sxs-lookup"><span data-stu-id="f59d1-234">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="f59d1-235">Leave the option **Automatically over the network** selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-235">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="f59d1-236">You can back up automatically over the network, or you can back up offline.</span><span class="sxs-lookup"><span data-stu-id="f59d1-236">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="f59d1-237">The remainder of this article describes the process for backing up automatically.</span><span class="sxs-lookup"><span data-stu-id="f59d1-237">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="f59d1-238">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span><span class="sxs-lookup"><span data-stu-id="f59d1-238">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="f59d1-239">On the Confirmation page, review the information, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-239">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="f59d1-240">After the wizard finishes creating the backup schedule, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-240">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="f59d1-241">To back up files and folders for the first time</span><span class="sxs-lookup"><span data-stu-id="f59d1-241">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="f59d1-242">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span><span class="sxs-lookup"><span data-stu-id="f59d1-242">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server back up now](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="f59d1-244">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span><span class="sxs-lookup"><span data-stu-id="f59d1-244">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="f59d1-245">Then click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="f59d1-245">Then click **Back Up**.</span></span>
3. <span data-ttu-id="f59d1-246">Click **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="f59d1-246">Click **Close** to close the wizard.</span></span> <span data-ttu-id="f59d1-247">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="f59d1-247">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="f59d1-248">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span><span class="sxs-lookup"><span data-stu-id="f59d1-248">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="f59d1-250">Questions?</span><span class="sxs-lookup"><span data-stu-id="f59d1-250">Questions?</span></span>
<span data-ttu-id="f59d1-251">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="f59d1-251">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f59d1-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="f59d1-252">Next steps</span></span>
* <span data-ttu-id="f59d1-253">Get more details about [backing up Windows machines](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-253">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="f59d1-254">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-254">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="f59d1-255">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f59d1-255">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>























