---
title: Delete a Recovery Services vault in Azure '
description: This article explains how to delete a Recovery Services vault. The article includes troubleshooting steps when you try to delete a vault, but can't.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 7/6/2018
ms.author: markgal
ms.openlocfilehash: 4dc5b006be8599177fb908fe022a3a821b137e12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809405"
---
# <a name="delete-a-recovery-services-vault"></a><span data-ttu-id="8b76d-104">Delete a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="8b76d-104">Delete a Recovery Services vault</span></span>

<span data-ttu-id="8b76d-105">This article explains how to remove all items from a Recovery Services vault, and then delete it.</span><span class="sxs-lookup"><span data-stu-id="8b76d-105">This article explains how to remove all items from a Recovery Services vault, and then delete it.</span></span> <span data-ttu-id="8b76d-106">You can't delete a Recovery Services vault if it is registered to a server and holds backup data.</span><span class="sxs-lookup"><span data-stu-id="8b76d-106">You can't delete a Recovery Services vault if it is registered to a server and holds backup data.</span></span> <span data-ttu-id="8b76d-107">If you try to delete a vault, but can't, the vault is still configured to receive backup data.</span><span class="sxs-lookup"><span data-stu-id="8b76d-107">If you try to delete a vault, but can't, the vault is still configured to receive backup data.</span></span>

<span data-ttu-id="8b76d-108">To learn how to delete a vault, see the section, [Delete a vault from Azure portal](backup-azure-delete-vault.md#delete-a-vault-from-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="8b76d-108">To learn how to delete a vault, see the section, [Delete a vault from Azure portal](backup-azure-delete-vault.md#delete-a-vault-from-azure-portal).</span></span> <span data-ttu-id="8b76d-109">If you don't want to retain any data in the Recovery Services vault, and want to delete the vault, see the section, [Delete the vault by force](backup-azure-delete-vault.md#delete-the-recovery-services-vault-by-force).</span><span class="sxs-lookup"><span data-stu-id="8b76d-109">If you don't want to retain any data in the Recovery Services vault, and want to delete the vault, see the section, [Delete the vault by force](backup-azure-delete-vault.md#delete-the-recovery-services-vault-by-force).</span></span> <span data-ttu-id="8b76d-110">If you aren't sure what's in the vault, and you need to make sure that you can delete the vault, see the section, [Remove vault dependencies and delete vault](backup-azure-delete-vault.md#remove-vault-dependencies-and-delete-vault).</span><span class="sxs-lookup"><span data-stu-id="8b76d-110">If you aren't sure what's in the vault, and you need to make sure that you can delete the vault, see the section, [Remove vault dependencies and delete vault](backup-azure-delete-vault.md#remove-vault-dependencies-and-delete-vault).</span></span>

## <a name="delete-a-vault-from-azure-portal"></a><span data-ttu-id="8b76d-111">Delete a vault from Azure portal</span><span class="sxs-lookup"><span data-stu-id="8b76d-111">Delete a vault from Azure portal</span></span>

<span data-ttu-id="8b76d-112">If you already have the Recovery Services vault open, skip to the second step.</span><span class="sxs-lookup"><span data-stu-id="8b76d-112">If you already have the Recovery Services vault open, skip to the second step.</span></span>

1. <span data-ttu-id="8b76d-113">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="8b76d-113">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span></span>

   <span data-ttu-id="8b76d-114">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **All Services** and in the list of resources, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-114">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **All Services** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="8b76d-115">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="8b76d-115">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="8b76d-116">To view the list of vaults in your subscription, click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-116">To view the list of vaults in your subscription, click **Recovery Services vaults**.</span></span>

   ![Create Recovery Services Vault step 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="8b76d-118">The list of Recovery Services vaults is displayed.</span><span class="sxs-lookup"><span data-stu-id="8b76d-118">The list of Recovery Services vaults is displayed.</span></span> 

   ![choose vault from list](./media/backup-azure-delete-vault/choose-vault-to-delete-.png)

1. <span data-ttu-id="8b76d-120">From the list, select the vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="8b76d-120">From the list, select the vault you want to delete.</span></span> <span data-ttu-id="8b76d-121">When you select the vault, its vault dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="8b76d-121">When you select the vault, its vault dashboard opens.</span></span>

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

1. <span data-ttu-id="8b76d-123">To delete a vault, in the vault dashboard, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-123">To delete a vault, in the vault dashboard, click **Delete**.</span></span> <span data-ttu-id="8b76d-124">You'll be asked to verify that you want to delete the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-124">You'll be asked to verify that you want to delete the vault.</span></span>

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/click-delete-button-to-delete-vault.png)

    <span data-ttu-id="8b76d-126">If the **Vault deletion error** appears, you can either remove the dependencies from the vault, or you can use PowerShell to delete the vault by force.</span><span class="sxs-lookup"><span data-stu-id="8b76d-126">If the **Vault deletion error** appears, you can either remove the dependencies from the vault, or you can use PowerShell to delete the vault by force.</span></span> <span data-ttu-id="8b76d-127">The following sections explain how to accomplish these tasks.</span><span class="sxs-lookup"><span data-stu-id="8b76d-127">The following sections explain how to accomplish these tasks.</span></span>

    ![Vault deletion error](./media/backup-azure-delete-vault/vault-delete-error.png)


## <a name="delete-the-recovery-services-vault-by-force"></a><span data-ttu-id="8b76d-129">Delete the Recovery Services vault by force</span><span class="sxs-lookup"><span data-stu-id="8b76d-129">Delete the Recovery Services vault by force</span></span>

<span data-ttu-id="8b76d-130">You can use PowerShell to delete a Recovery Services vault by force.</span><span class="sxs-lookup"><span data-stu-id="8b76d-130">You can use PowerShell to delete a Recovery Services vault by force.</span></span> <span data-ttu-id="8b76d-131">By force means the Recovery Services vault, and all associated backup data, is permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="8b76d-131">By force means the Recovery Services vault, and all associated backup data, is permanently deleted.</span></span> 

> [!Warning]
> <span data-ttu-id="8b76d-132">When using PowerShell to delete a Recovery Services vault, be certain that you want to permanently delete all backup data in the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-132">When using PowerShell to delete a Recovery Services vault, be certain that you want to permanently delete all backup data in the vault.</span></span>
>

<span data-ttu-id="8b76d-133">To delete a Recovery Services vault:</span><span class="sxs-lookup"><span data-stu-id="8b76d-133">To delete a Recovery Services vault:</span></span>

1. <span data-ttu-id="8b76d-134">Sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="8b76d-134">Sign in to your Azure account.</span></span>

   <span data-ttu-id="8b76d-135">Sign in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="8b76d-135">Sign in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

   ```powershell
    Connect-AzureRmAccount
   ```
   <span data-ttu-id="8b76d-136">The first time you use Azure Backup, you must register the Azure Recovery Service provider in your subscription with [Register-AzureRmResourceProvider](/powershell/module/AzureRM.Resources/Register-AzureRmResourceProvider).</span><span class="sxs-lookup"><span data-stu-id="8b76d-136">The first time you use Azure Backup, you must register the Azure Recovery Service provider in your subscription with [Register-AzureRmResourceProvider](/powershell/module/AzureRM.Resources/Register-AzureRmResourceProvider).</span></span>

   ```powershell
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
   ```

1. <span data-ttu-id="8b76d-137">Open a PowerShell window with Administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="8b76d-137">Open a PowerShell window with Administrator privileges.</span></span>

1. <span data-ttu-id="8b76d-138">Use `Set-ExecutionPolicy Unrestricted` to remove any restrictions.</span><span class="sxs-lookup"><span data-stu-id="8b76d-138">Use `Set-ExecutionPolicy Unrestricted` to remove any restrictions.</span></span>

1. <span data-ttu-id="8b76d-139">Run the following command to download the Azure Resource Manager Client package from chocolately.org.</span><span class="sxs-lookup"><span data-stu-id="8b76d-139">Run the following command to download the Azure Resource Manager Client package from chocolately.org.</span></span>

    `iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

1. <span data-ttu-id="8b76d-140">Use the following command to install the Azure Resource Manager API Client.</span><span class="sxs-lookup"><span data-stu-id="8b76d-140">Use the following command to install the Azure Resource Manager API Client.</span></span>

   `choco.exe install armclient`

1. <span data-ttu-id="8b76d-141">In the Azure portal, gather the Subscription ID and associated resource group name for the Recovery Services vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="8b76d-141">In the Azure portal, gather the Subscription ID and associated resource group name for the Recovery Services vault you want to delete.</span></span>

1. <span data-ttu-id="8b76d-142">In PowerShell, run the following command using your subscription ID, resource group name, and Recovery Services vault name.</span><span class="sxs-lookup"><span data-stu-id="8b76d-142">In PowerShell, run the following command using your subscription ID, resource group name, and Recovery Services vault name.</span></span> <span data-ttu-id="8b76d-143">When you run the command, it deletes the vault and all dependencies.</span><span class="sxs-lookup"><span data-stu-id="8b76d-143">When you run the command, it deletes the vault and all dependencies.</span></span>

   ```powershell
   ARMClient.exe delete /subscriptions/<subscriptionID>/resourceGroups/<resourcegroupname>/providers/Microsoft.RecoveryServices/vaults/<recovery services vault name>?api-version=2015-03-15
   ```
1. <span data-ttu-id="8b76d-144">Sign in to your subscription in the Azure portal and verify the vault is deleted.</span><span class="sxs-lookup"><span data-stu-id="8b76d-144">Sign in to your subscription in the Azure portal and verify the vault is deleted.</span></span>


## <a name="remove-vault-dependencies-and-delete-vault"></a><span data-ttu-id="8b76d-145">Remove vault dependencies and delete vault</span><span class="sxs-lookup"><span data-stu-id="8b76d-145">Remove vault dependencies and delete vault</span></span>

<span data-ttu-id="8b76d-146">To manually remove the vault dependencies, delete the configuration between each item or server, and Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-146">To manually remove the vault dependencies, delete the configuration between each item or server, and Recovery Services vault.</span></span> <span data-ttu-id="8b76d-147">As you go through the following procedure, use the **Backup Items** menu (see image) for:</span><span class="sxs-lookup"><span data-stu-id="8b76d-147">As you go through the following procedure, use the **Backup Items** menu (see image) for:</span></span>

* <span data-ttu-id="8b76d-148">Azure Storage (Azure Files) backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-148">Azure Storage (Azure Files) backups</span></span>
* <span data-ttu-id="8b76d-149">SQL Server in Azure VM backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-149">SQL Server in Azure VM backups</span></span>
* <span data-ttu-id="8b76d-150">Azure virtual machines backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-150">Azure virtual machines backups</span></span>
* <span data-ttu-id="8b76d-151">Microsoft Azure Recovery Services agent backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-151">Microsoft Azure Recovery Services agent backups</span></span>

<span data-ttu-id="8b76d-152">Use the **Backup Infrastructure** menu (see image) for:</span><span class="sxs-lookup"><span data-stu-id="8b76d-152">Use the **Backup Infrastructure** menu (see image) for:</span></span>

* <span data-ttu-id="8b76d-153">Azure Backup Server backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-153">Azure Backup Server backups</span></span>
* <span data-ttu-id="8b76d-154">System Center DPM backups</span><span class="sxs-lookup"><span data-stu-id="8b76d-154">System Center DPM backups</span></span>

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/backup-items-backup-infrastructure.png)

1. <span data-ttu-id="8b76d-156">In the vault dashboard menu, scroll down to the Protected Items section, and click **Backup Items**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-156">In the vault dashboard menu, scroll down to the Protected Items section, and click **Backup Items**.</span></span> <span data-ttu-id="8b76d-157">In this menu, you can stop and delete Azure File Servers, SQL Servers in Azure VM, and Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8b76d-157">In this menu, you can stop and delete Azure File Servers, SQL Servers in Azure VM, and Azure virtual machines.</span></span> <span data-ttu-id="8b76d-158">In this example, we'll remove backup data from an Azure File Server.</span><span class="sxs-lookup"><span data-stu-id="8b76d-158">In this example, we'll remove backup data from an Azure File Server.</span></span>

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/selected-backup-items.png)

1. <span data-ttu-id="8b76d-160">Select a backup type to view all items of that type.</span><span class="sxs-lookup"><span data-stu-id="8b76d-160">Select a backup type to view all items of that type.</span></span>

    ![select the backup type](./media/backup-azure-delete-vault/azure-storage-selected-list.png)

1. <span data-ttu-id="8b76d-162">For all items in the list, right-click the item, and from the context menu, select **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-162">For all items in the list, right-click the item, and from the context menu, select **Stop backup**.</span></span>

    ![select the backup type](./media/backup-azure-delete-vault/stop-backup-item.png) 

    <span data-ttu-id="8b76d-164">The Stop Backup menu opens.</span><span class="sxs-lookup"><span data-stu-id="8b76d-164">The Stop Backup menu opens.</span></span>

1. <span data-ttu-id="8b76d-165">On the **Stop Backup** menu, from the **Choose an option** menu, select **Delete Backup Data**, type the name of the item, and click **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-165">On the **Stop Backup** menu, from the **Choose an option** menu, select **Delete Backup Data**, type the name of the item, and click **Stop backup**.</span></span>

    <span data-ttu-id="8b76d-166">Type the name of the item, to verify you want to delete it.</span><span class="sxs-lookup"><span data-stu-id="8b76d-166">Type the name of the item, to verify you want to delete it.</span></span> <span data-ttu-id="8b76d-167">The **Stop Backup** button activates once you verify the item.</span><span class="sxs-lookup"><span data-stu-id="8b76d-167">The **Stop Backup** button activates once you verify the item.</span></span> <span data-ttu-id="8b76d-168">If you retain the data, you won't be able to delete the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-168">If you retain the data, you won't be able to delete the vault.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="8b76d-170">If you want, provide a reason why you're deleting the data, and add comments.</span><span class="sxs-lookup"><span data-stu-id="8b76d-170">If you want, provide a reason why you're deleting the data, and add comments.</span></span> <span data-ttu-id="8b76d-171">To verify the job completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span><span class="sxs-lookup"><span data-stu-id="8b76d-171">To verify the job completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="8b76d-172">Once the job completes, the service sends a message: *the backup process was stopped and the backup data was deleted*.</span><span class="sxs-lookup"><span data-stu-id="8b76d-172">Once the job completes, the service sends a message: *the backup process was stopped and the backup data was deleted*.</span></span>

1. <span data-ttu-id="8b76d-173">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the items in the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-173">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the items in the vault.</span></span>

      ![delete backup data](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="8b76d-175">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-175">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span></span> <span data-ttu-id="8b76d-176">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span><span class="sxs-lookup"><span data-stu-id="8b76d-176">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="8b76d-177">If items still appear in the vault, return to step three and choose a different item type list.</span><span class="sxs-lookup"><span data-stu-id="8b76d-177">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  

1. <span data-ttu-id="8b76d-178">When there are no more items in the vault toolbar, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-178">When there are no more items in the vault toolbar, click **Delete**.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/vault-ready-to-delete.png)

1. <span data-ttu-id="8b76d-180">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-180">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="8b76d-181">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-181">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="removing-azure-backup-server-or-dpm"></a><span data-ttu-id="8b76d-182">Removing Azure Backup Server or DPM</span><span class="sxs-lookup"><span data-stu-id="8b76d-182">Removing Azure Backup Server or DPM</span></span>

1. <span data-ttu-id="8b76d-183">In the vault dashboard menu, scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-183">In the vault dashboard menu, scroll down to the Manage section, and click **Backup Infrastructure**.</span></span> 

1. <span data-ttu-id="8b76d-184">In the submenu, click **Backup Management Servers** to view the Azure Backup Servers and System Center DPM server.</span><span class="sxs-lookup"><span data-stu-id="8b76d-184">In the submenu, click **Backup Management Servers** to view the Azure Backup Servers and System Center DPM server.</span></span> <span data-ttu-id="8b76d-185">you can stop and delete Azure File Servers, SQL Servers in Azure VM, and Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8b76d-185">you can stop and delete Azure File Servers, SQL Servers in Azure VM, and Azure virtual machines.</span></span> 

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/delete-backup-management-servers.png)

1. <span data-ttu-id="8b76d-187">Right-click the item you want to delete, and from the sub-menu, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-187">Right-click the item you want to delete, and from the sub-menu, select **Delete**.</span></span>

    ![select the backup type](./media/backup-azure-delete-vault/azure-storage-selected-list.png)

    <span data-ttu-id="8b76d-189">The Stop Backup menu opens.</span><span class="sxs-lookup"><span data-stu-id="8b76d-189">The Stop Backup menu opens.</span></span>

1. <span data-ttu-id="8b76d-190">On the **Stop Backup** menu, from the **Choose an option** menu, select **Delete Backup Data**, type the name of the item, and click **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-190">On the **Stop Backup** menu, from the **Choose an option** menu, select **Delete Backup Data**, type the name of the item, and click **Stop backup**.</span></span>

    <span data-ttu-id="8b76d-191">To verify you want to delete, type its name.</span><span class="sxs-lookup"><span data-stu-id="8b76d-191">To verify you want to delete, type its name.</span></span> <span data-ttu-id="8b76d-192">The **Stop Backup** button activates once you verify the item.</span><span class="sxs-lookup"><span data-stu-id="8b76d-192">The **Stop Backup** button activates once you verify the item.</span></span> <span data-ttu-id="8b76d-193">If you retain the data, you can't delete the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-193">If you retain the data, you can't delete the vault.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="8b76d-195">Optionally, you can provide a reason why you are deleting the data, and add comments.</span><span class="sxs-lookup"><span data-stu-id="8b76d-195">Optionally, you can provide a reason why you are deleting the data, and add comments.</span></span> <span data-ttu-id="8b76d-196">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span><span class="sxs-lookup"><span data-stu-id="8b76d-196">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="8b76d-197">Once the job is complete, the service sends a message: the backup process was stopped and the backup data was deleted.</span><span class="sxs-lookup"><span data-stu-id="8b76d-197">Once the job is complete, the service sends a message: the backup process was stopped and the backup data was deleted.</span></span>

1. <span data-ttu-id="8b76d-198">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-198">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span></span>

      ![delete backup data](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="8b76d-200">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-200">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span></span> <span data-ttu-id="8b76d-201">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span><span class="sxs-lookup"><span data-stu-id="8b76d-201">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="8b76d-202">If items still appear in the vault, return to step three and choose a different item type list.</span><span class="sxs-lookup"><span data-stu-id="8b76d-202">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  
1. <span data-ttu-id="8b76d-203">When there are no more items in the vault, on the vault dashboard click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-203">When there are no more items in the vault, on the vault dashboard click **Delete**.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/vault-ready-to-delete.png)

1. <span data-ttu-id="8b76d-205">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-205">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="8b76d-206">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-206">The vault is deleted and the portal returns to the **New** service menu.</span></span>


## <a name="removing-azure-backup-agent-recovery-points"></a><span data-ttu-id="8b76d-207">Removing Azure Backup agent recovery points</span><span class="sxs-lookup"><span data-stu-id="8b76d-207">Removing Azure Backup agent recovery points</span></span>

1. <span data-ttu-id="8b76d-208">In the vault dashboard menu, scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-208">In the vault dashboard menu, scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

1. <span data-ttu-id="8b76d-209">In the sub-menu, click **Protected Servers** to view the list of protected server types, including Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="8b76d-209">In the sub-menu, click **Protected Servers** to view the list of protected server types, including Azure Backup agent.</span></span>

    ![select your vault to open its dashboard](./media/backup-azure-delete-vault/identify-protected-servers.png)

1. <span data-ttu-id="8b76d-211">In the **Protected Servers** list, click Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="8b76d-211">In the **Protected Servers** list, click Azure Backup Agent.</span></span>

    ![select the backup type](./media/backup-azure-delete-vault/list-of-protected-server-types.png)

    <span data-ttu-id="8b76d-213">The list of servers protected using Azure Backup agent, opens.</span><span class="sxs-lookup"><span data-stu-id="8b76d-213">The list of servers protected using Azure Backup agent, opens.</span></span>

    ![select the specific protected server](./media/backup-azure-delete-vault/azure-backup-agent-protected-servers.png)

1. <span data-ttu-id="8b76d-215">In the list of servers, click one to open its menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-215">In the list of servers, click one to open its menu.</span></span>

    ![view the selected server's dashboard](./media/backup-azure-delete-vault/selected-protected-server.png)

1. <span data-ttu-id="8b76d-217">On the selected server's dashboard menu, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-217">On the selected server's dashboard menu, click **Delete**.</span></span>

    ![delete the selected server](./media/backup-azure-delete-vault/selected-protected-server-click-delete.png)

1. <span data-ttu-id="8b76d-219">On the **Delete** menu, type the name of the item, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-219">On the **Delete** menu, type the name of the item, and click **Delete**.</span></span>

    <span data-ttu-id="8b76d-220">Type the name of the item, to verify you want to delete it.</span><span class="sxs-lookup"><span data-stu-id="8b76d-220">Type the name of the item, to verify you want to delete it.</span></span> <span data-ttu-id="8b76d-221">The **Delete** button activates once you verify the item.</span><span class="sxs-lookup"><span data-stu-id="8b76d-221">The **Delete** button activates once you verify the item.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/delete-protected-server-dialog.png)

    <span data-ttu-id="8b76d-223">Optionally, you can provide a reason why you are deleting the data, and add comments.</span><span class="sxs-lookup"><span data-stu-id="8b76d-223">Optionally, you can provide a reason why you are deleting the data, and add comments.</span></span> <span data-ttu-id="8b76d-224">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span><span class="sxs-lookup"><span data-stu-id="8b76d-224">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="8b76d-225">Once the job is complete, the service sends a message: the backup process was stopped and the backup data was deleted.</span><span class="sxs-lookup"><span data-stu-id="8b76d-225">Once the job is complete, the service sends a message: the backup process was stopped and the backup data was deleted.</span></span>

1. <span data-ttu-id="8b76d-226">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-226">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span></span>

      ![delete backup data](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="8b76d-228">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-228">When there are no items in the list, scroll to the **Essentials** pane in the Recovery Services vault menu.</span></span> <span data-ttu-id="8b76d-229">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span><span class="sxs-lookup"><span data-stu-id="8b76d-229">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="8b76d-230">If items still appear in the vault, return to step three and choose a different item type list.</span><span class="sxs-lookup"><span data-stu-id="8b76d-230">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  
1. <span data-ttu-id="8b76d-231">When there are no more items in the vault, on the vault dashboard click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-231">When there are no more items in the vault, on the vault dashboard click **Delete**.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/vault-ready-to-delete.png)

1. <span data-ttu-id="8b76d-233">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-233">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="8b76d-234">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="8b76d-234">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="what-if-i-stop-the-backup-process-but-retain-the-data"></a><span data-ttu-id="8b76d-235">What if I stop the backup process but retain the data?</span><span class="sxs-lookup"><span data-stu-id="8b76d-235">What if I stop the backup process but retain the data?</span></span>

<span data-ttu-id="8b76d-236">If you stop the backup process but accidentally *retain* the data, you must delete the backup data before you can delete the vault.</span><span class="sxs-lookup"><span data-stu-id="8b76d-236">If you stop the backup process but accidentally *retain* the data, you must delete the backup data before you can delete the vault.</span></span> <span data-ttu-id="8b76d-237">To delete the backup data:</span><span class="sxs-lookup"><span data-stu-id="8b76d-237">To delete the backup data:</span></span>

1. <span data-ttu-id="8b76d-238">On the **Backup Items** menu, right-click the item, and on the context menu click **Delete backup data**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-238">On the **Backup Items** menu, right-click the item, and on the context menu click **Delete backup data**.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="8b76d-240">The **Delete Backup Data** menu opens.</span><span class="sxs-lookup"><span data-stu-id="8b76d-240">The **Delete Backup Data** menu opens.</span></span>
1. <span data-ttu-id="8b76d-241">On the **Delete Backup Data** menu, type the name of the item, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8b76d-241">On the **Delete Backup Data** menu, type the name of the item, and click **Delete**.</span></span>

    ![delete backup data](./media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="8b76d-243">Once you have deleted the data, return to step 4c and continue with the process.</span><span class="sxs-lookup"><span data-stu-id="8b76d-243">Once you have deleted the data, return to step 4c and continue with the process.</span></span>
