---
title: " Delete a Backup vault in Azure | Microsoft Docs "
description: How to delete an Azure Backup and Recovery Services vault. A backup vault can be called an Azure cloud vault, or Azure recovery vault. Troubleshooting problems when you can't delete a backup vault in the classic portal or Azure portal.
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: ''
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 3/14/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 3ec1d5a3e6a488ea61ede0a58aa3d2abea692d1b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555688"
---
# <a name="delete-an-azure-backup-vault"></a><span data-ttu-id="03dbb-105">Delete an Azure Backup vault</span><span class="sxs-lookup"><span data-stu-id="03dbb-105">Delete an Azure Backup vault</span></span>
<span data-ttu-id="03dbb-106">The Azure Backup service has two types of vaults - the Backup vault and the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-106">The Azure Backup service has two types of vaults - the Backup vault and the Recovery Services vault.</span></span> <span data-ttu-id="03dbb-107">The Backup vault came first.</span><span class="sxs-lookup"><span data-stu-id="03dbb-107">The Backup vault came first.</span></span> <span data-ttu-id="03dbb-108">Then the Recovery Services vault came along to support the expanded Resource Manager deployments.</span><span class="sxs-lookup"><span data-stu-id="03dbb-108">Then the Recovery Services vault came along to support the expanded Resource Manager deployments.</span></span> <span data-ttu-id="03dbb-109">Because of the expanded capabilities and the information dependencies that must be stored in the vault, deleting a Backup or Recovery Services vault can be confusing.</span><span class="sxs-lookup"><span data-stu-id="03dbb-109">Because of the expanded capabilities and the information dependencies that must be stored in the vault, deleting a Backup or Recovery Services vault can be confusing.</span></span> <span data-ttu-id="03dbb-110">This article explains how to delete the vaults in the classic portal and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03dbb-110">This article explains how to delete the vaults in the classic portal and the Azure portal.</span></span>  

| <span data-ttu-id="03dbb-111">**Deployment Type**</span><span class="sxs-lookup"><span data-stu-id="03dbb-111">**Deployment Type**</span></span> | <span data-ttu-id="03dbb-112">**Portal**</span><span class="sxs-lookup"><span data-stu-id="03dbb-112">**Portal**</span></span> | <span data-ttu-id="03dbb-113">**Vault name**</span><span class="sxs-lookup"><span data-stu-id="03dbb-113">**Vault name**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03dbb-114">Classic</span><span class="sxs-lookup"><span data-stu-id="03dbb-114">Classic</span></span> |<span data-ttu-id="03dbb-115">Classic</span><span class="sxs-lookup"><span data-stu-id="03dbb-115">Classic</span></span> |<span data-ttu-id="03dbb-116">Backup vault</span><span class="sxs-lookup"><span data-stu-id="03dbb-116">Backup vault</span></span> |
| <span data-ttu-id="03dbb-117">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03dbb-117">Resource Manager</span></span> |<span data-ttu-id="03dbb-118">Azure</span><span class="sxs-lookup"><span data-stu-id="03dbb-118">Azure</span></span> |<span data-ttu-id="03dbb-119">Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="03dbb-119">Recovery Services vault</span></span> |

> [!NOTE]
> <span data-ttu-id="03dbb-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span><span class="sxs-lookup"><span data-stu-id="03dbb-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span></span> <span data-ttu-id="03dbb-121">However, you can use a Recovery Services vault to protect classically deployed servers and VMs.</span><span class="sxs-lookup"><span data-stu-id="03dbb-121">However, you can use a Recovery Services vault to protect classically deployed servers and VMs.</span></span>  
>
>

<span data-ttu-id="03dbb-122">In this article, we use the term, vault, to refer to the generic form of the Backup vault or Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-122">In this article, we use the term, vault, to refer to the generic form of the Backup vault or Recovery Services vault.</span></span> <span data-ttu-id="03dbb-123">We use the formal name, Backup vault, or Recovery Services vault, when it is necessary to distinguish between the vaults.</span><span class="sxs-lookup"><span data-stu-id="03dbb-123">We use the formal name, Backup vault, or Recovery Services vault, when it is necessary to distinguish between the vaults.</span></span>

## <a name="deleting-a-recovery-services-vault"></a><span data-ttu-id="03dbb-124">Deleting a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="03dbb-124">Deleting a Recovery Services vault</span></span>
<span data-ttu-id="03dbb-125">Deleting a Recovery Services vault is a one-step process - *provided the vault doesn't contain any resources*.</span><span class="sxs-lookup"><span data-stu-id="03dbb-125">Deleting a Recovery Services vault is a one-step process - *provided the vault doesn't contain any resources*.</span></span> <span data-ttu-id="03dbb-126">Before you can delete a Recovery Services vault, you must remove or delete all resources in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-126">Before you can delete a Recovery Services vault, you must remove or delete all resources in the vault.</span></span> <span data-ttu-id="03dbb-127">If you attepmt to delete a vault that contains resources, you get an error like the following image:</span><span class="sxs-lookup"><span data-stu-id="03dbb-127">If you attepmt to delete a vault that contains resources, you get an error like the following image:</span></span>

![Vault deletion error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

<span data-ttu-id="03dbb-129">Until you have cleared the resources from the vault, clicking **Retry** produces the same error.</span><span class="sxs-lookup"><span data-stu-id="03dbb-129">Until you have cleared the resources from the vault, clicking **Retry** produces the same error.</span></span> <span data-ttu-id="03dbb-130">If you're stuck on this error message, click **Cancel** and use the following steps to delete the resources in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-130">If you're stuck on this error message, click **Cancel** and use the following steps to delete the resources in the vault.</span></span>

### <a name="removing-the-items-from-a-vault-protecting-a-vm"></a><span data-ttu-id="03dbb-131">Removing the items from a vault protecting a VM</span><span class="sxs-lookup"><span data-stu-id="03dbb-131">Removing the items from a vault protecting a VM</span></span>
<span data-ttu-id="03dbb-132">If you already have the Recovery Services vault open, skip to the second step.</span><span class="sxs-lookup"><span data-stu-id="03dbb-132">If you already have the Recovery Services vault open, skip to the second step.</span></span>

1. <span data-ttu-id="03dbb-133">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="03dbb-133">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span></span>

   <span data-ttu-id="03dbb-134">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **More Services** and in the list of resources, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-134">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **More Services** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="03dbb-135">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="03dbb-135">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="03dbb-136">Click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-136">Click **Recovery Services vaults**.</span></span>

   ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="03dbb-138">The list of Recovery Services vaults is displayed.</span><span class="sxs-lookup"><span data-stu-id="03dbb-138">The list of Recovery Services vaults is displayed.</span></span> <span data-ttu-id="03dbb-139">From the list, select the vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="03dbb-139">From the list, select the vault you want to delete.</span></span>

   ![choose vault from list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. <span data-ttu-id="03dbb-141">In the vault view, look at the **Essentials** pane.</span><span class="sxs-lookup"><span data-stu-id="03dbb-141">In the vault view, look at the **Essentials** pane.</span></span> <span data-ttu-id="03dbb-142">To delete a vault, there cannot be any protected items.</span><span class="sxs-lookup"><span data-stu-id="03dbb-142">To delete a vault, there cannot be any protected items.</span></span> <span data-ttu-id="03dbb-143">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-143">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete the vault.</span></span>

    ![Look at Essentials pane for protected items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    <span data-ttu-id="03dbb-145">VMs and Files/Folders are considered Backup Items, and are listed in the **Backup Items** area of the Essentials pane.</span><span class="sxs-lookup"><span data-stu-id="03dbb-145">VMs and Files/Folders are considered Backup Items, and are listed in the **Backup Items** area of the Essentials pane.</span></span> <span data-ttu-id="03dbb-146">A DPM server is listed in the **Backup Management Server** area of the Essentials pane.</span><span class="sxs-lookup"><span data-stu-id="03dbb-146">A DPM server is listed in the **Backup Management Server** area of the Essentials pane.</span></span> <span data-ttu-id="03dbb-147">**Replicated Items** pertain to the Azure Site Recovery service.</span><span class="sxs-lookup"><span data-stu-id="03dbb-147">**Replicated Items** pertain to the Azure Site Recovery service.</span></span>
3. <span data-ttu-id="03dbb-148">To begin removing the protected items from the vault, find the items in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-148">To begin removing the protected items from the vault, find the items in the vault.</span></span> <span data-ttu-id="03dbb-149">In the vault dashboard click **Settings**, and then click **Backup items** to open that blade.</span><span class="sxs-lookup"><span data-stu-id="03dbb-149">In the vault dashboard click **Settings**, and then click **Backup items** to open that blade.</span></span>

    ![choose vault from list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    <span data-ttu-id="03dbb-151">The **Backup Items** blade has separate lists, based on the Item Type: Azure Virtual Machines or File-Folders (see image).</span><span class="sxs-lookup"><span data-stu-id="03dbb-151">The **Backup Items** blade has separate lists, based on the Item Type: Azure Virtual Machines or File-Folders (see image).</span></span> <span data-ttu-id="03dbb-152">The default Item Type list shown is Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="03dbb-152">The default Item Type list shown is Azure Virtual Machines.</span></span> <span data-ttu-id="03dbb-153">To view the list of File-Folders items in the vault, select **File-Folders** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="03dbb-153">To view the list of File-Folders items in the vault, select **File-Folders** from the drop-down menu.</span></span>
4. <span data-ttu-id="03dbb-154">Before you can delete an item from the vault protecting a VM, you must stop the item's backup job and delete the recovery point data.</span><span class="sxs-lookup"><span data-stu-id="03dbb-154">Before you can delete an item from the vault protecting a VM, you must stop the item's backup job and delete the recovery point data.</span></span> <span data-ttu-id="03dbb-155">For each item in the vault, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="03dbb-155">For each item in the vault, follow these steps:</span></span>

    <span data-ttu-id="03dbb-156">a.</span><span class="sxs-lookup"><span data-stu-id="03dbb-156">a.</span></span> <span data-ttu-id="03dbb-157">On the **Backup Items** blade, right-click the item, and from the context menu, select **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-157">On the **Backup Items** blade, right-click the item, and from the context menu, select **Stop backup**.</span></span>

    ![stop the backup job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/stop-the-backup-process.png)

    <span data-ttu-id="03dbb-159">The Stop Backup blade opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-159">The Stop Backup blade opens.</span></span>

    <span data-ttu-id="03dbb-160">b.</span><span class="sxs-lookup"><span data-stu-id="03dbb-160">b.</span></span> <span data-ttu-id="03dbb-161">On the **Stop Backup** blade, from the **Choose an option** menu, select **Delete Backup Data** > type the name of the item > and click **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-161">On the **Stop Backup** blade, from the **Choose an option** menu, select **Delete Backup Data** > type the name of the item > and click **Stop backup**.</span></span>

    <span data-ttu-id="03dbb-162">Type the name of the item, to verify you want to delete it.</span><span class="sxs-lookup"><span data-stu-id="03dbb-162">Type the name of the item, to verify you want to delete it.</span></span> <span data-ttu-id="03dbb-163">The **Stop Backup** button activates once you verify the item.</span><span class="sxs-lookup"><span data-stu-id="03dbb-163">The **Stop Backup** button activates once you verify the item.</span></span> <span data-ttu-id="03dbb-164">If you do not see the dialog box to type the name of the backup item, you chose the **Retain Backup Data** option.</span><span class="sxs-lookup"><span data-stu-id="03dbb-164">If you do not see the dialog box to type the name of the backup item, you chose the **Retain Backup Data** option.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="03dbb-166">Optionally, you can provide a reason why you are deleting the data, and add comments.</span><span class="sxs-lookup"><span data-stu-id="03dbb-166">Optionally, you can provide a reason why you are deleting the data, and add comments.</span></span> <span data-ttu-id="03dbb-167">After you click **Stop Backup**, allow the delete job to complete before attempting to delete the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-167">After you click **Stop Backup**, allow the delete job to complete before attempting to delete the vault.</span></span> <span data-ttu-id="03dbb-168">To verify that the job has completed, check the Azure Messages ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/messages.png).</span><span class="sxs-lookup"><span data-stu-id="03dbb-168">To verify that the job has completed, check the Azure Messages ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="03dbb-169">Once the job is complete, you receive a message stating the backup process was stopped and the backup data, for that item, was deleted.</span><span class="sxs-lookup"><span data-stu-id="03dbb-169">Once the job is complete, you receive a message stating the backup process was stopped and the backup data, for that item, was deleted.</span></span>

    <span data-ttu-id="03dbb-170">c.</span><span class="sxs-lookup"><span data-stu-id="03dbb-170">c.</span></span> <span data-ttu-id="03dbb-171">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-171">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span></span>

      ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="03dbb-173">When there are no items in the list, scroll to the **Essentials** pane in the Backup vault blade.</span><span class="sxs-lookup"><span data-stu-id="03dbb-173">When there are no items in the list, scroll to the **Essentials** pane in the Backup vault blade.</span></span> <span data-ttu-id="03dbb-174">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span><span class="sxs-lookup"><span data-stu-id="03dbb-174">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="03dbb-175">If items still appear in the vault, return to step three and choose a different item type list.</span><span class="sxs-lookup"><span data-stu-id="03dbb-175">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  
5. <span data-ttu-id="03dbb-176">When there are no more items in the vault toolbar, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-176">When there are no more items in the vault toolbar, click **Delete**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-vault.png)
6. <span data-ttu-id="03dbb-178">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-178">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="03dbb-179">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="03dbb-179">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="what-if-i-stopped-the-backup-process-but-retained-the-data"></a><span data-ttu-id="03dbb-180">What if I stopped the backup process but retained the data?</span><span class="sxs-lookup"><span data-stu-id="03dbb-180">What if I stopped the backup process but retained the data?</span></span>
<span data-ttu-id="03dbb-181">If you stopped the backup process but accidentally *retained* the data, you must delete the backup data before you can delete the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-181">If you stopped the backup process but accidentally *retained* the data, you must delete the backup data before you can delete the vault.</span></span> <span data-ttu-id="03dbb-182">To delete the backup data:</span><span class="sxs-lookup"><span data-stu-id="03dbb-182">To delete the backup data:</span></span>

1. <span data-ttu-id="03dbb-183">On the **Backup Items** blade, right-click the item, and on the context menu click **Delete backup data**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-183">On the **Backup Items** blade, right-click the item, and on the context menu click **Delete backup data**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="03dbb-185">The **Delete Backup Data** blade opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-185">The **Delete Backup Data** blade opens.</span></span>
2. <span data-ttu-id="03dbb-186">On the **Delete Backup Data** blade, type the name of the item, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-186">On the **Delete Backup Data** blade, type the name of the item, and click **Delete**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="03dbb-188">Once you have deleted the data, return to step 4c and continue with the process.</span><span class="sxs-lookup"><span data-stu-id="03dbb-188">Once you have deleted the data, return to step 4c and continue with the process.</span></span>

## <a name="delete-a-vault-used-to-protect-a-dpm-server"></a><span data-ttu-id="03dbb-189">Delete a vault used to protect a DPM server</span><span class="sxs-lookup"><span data-stu-id="03dbb-189">Delete a vault used to protect a DPM server</span></span>
<span data-ttu-id="03dbb-190">Before you can delete a vault used to protect a DPM server, you must clear any recovery points that have been created, and then unregister the server from the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-190">Before you can delete a vault used to protect a DPM server, you must clear any recovery points that have been created, and then unregister the server from the vault.</span></span>

<span data-ttu-id="03dbb-191">To delete the data associated with a protection group:</span><span class="sxs-lookup"><span data-stu-id="03dbb-191">To delete the data associated with a protection group:</span></span>

1. <span data-ttu-id="03dbb-192">In the DPM Administrator Console, click **Protection** > select a protection group > select the Protection Group Member > and in the tool ribbon, click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-192">In the DPM Administrator Console, click **Protection** > select a protection group > select the Protection Group Member > and in the tool ribbon, click **Remove**.</span></span>

  <span data-ttu-id="03dbb-193">Select the Protection Group Member to activate the **Remove** button in the tool ribbon.</span><span class="sxs-lookup"><span data-stu-id="03dbb-193">Select the Protection Group Member to activate the **Remove** button in the tool ribbon.</span></span> <span data-ttu-id="03dbb-194">In the example, the member is **dummyvm9**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-194">In the example, the member is **dummyvm9**.</span></span> <span data-ttu-id="03dbb-195">To select multiple members in the protection group, hold down the Ctrl key while clicking on the members.</span><span class="sxs-lookup"><span data-stu-id="03dbb-195">To select multiple members in the protection group, hold down the Ctrl key while clicking on the members.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    <span data-ttu-id="03dbb-197">The **Stop Protection** dialog opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-197">The **Stop Protection** dialog opens.</span></span>
2. <span data-ttu-id="03dbb-198">In the **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-198">In the **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    <span data-ttu-id="03dbb-200">To delete a vault, you must clear, or delete, the vault of protected data.</span><span class="sxs-lookup"><span data-stu-id="03dbb-200">To delete a vault, you must clear, or delete, the vault of protected data.</span></span> <span data-ttu-id="03dbb-201">Depending on the number of recovery points and data in the protection group, it may take anywhere from a few seconds to several minutes to delete the data.</span><span class="sxs-lookup"><span data-stu-id="03dbb-201">Depending on the number of recovery points and data in the protection group, it may take anywhere from a few seconds to several minutes to delete the data.</span></span> <span data-ttu-id="03dbb-202">The **Stop Protection** dialog shows the status when the job has completed.</span><span class="sxs-lookup"><span data-stu-id="03dbb-202">The **Stop Protection** dialog shows the status when the job has completed.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. <span data-ttu-id="03dbb-204">Continue this process for all members in all protection groups.</span><span class="sxs-lookup"><span data-stu-id="03dbb-204">Continue this process for all members in all protection groups.</span></span>

    <span data-ttu-id="03dbb-205">Remove all protected data and protection groups.</span><span class="sxs-lookup"><span data-stu-id="03dbb-205">Remove all protected data and protection groups.</span></span>
4. <span data-ttu-id="03dbb-206">After deleting all members from the protection group, switch to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03dbb-206">After deleting all members from the protection group, switch to the Azure portal.</span></span> <span data-ttu-id="03dbb-207">Open the vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-207">Open the vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="03dbb-208">On the vault toolbar, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-208">On the vault toolbar, click **Delete**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-vault.png)

    <span data-ttu-id="03dbb-210">If there are Backup management servers registered to the vault, you can't delete the vault even if there is no data in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-210">If there are Backup management servers registered to the vault, you can't delete the vault even if there is no data in the vault.</span></span> <span data-ttu-id="03dbb-211">If you deleted the Backup management servers associated with the vault, but there are servers listed in the **Essentials** pane, see [Find the Backup management servers registered to the vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span><span class="sxs-lookup"><span data-stu-id="03dbb-211">If you deleted the Backup management servers associated with the vault, but there are servers listed in the **Essentials** pane, see [Find the Backup management servers registered to the vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span></span>
5. <span data-ttu-id="03dbb-212">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-212">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="03dbb-213">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="03dbb-213">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-vault-used-to-protect-a-production-server"></a><span data-ttu-id="03dbb-214">Delete a vault used to protect a Production server</span><span class="sxs-lookup"><span data-stu-id="03dbb-214">Delete a vault used to protect a Production server</span></span>
<span data-ttu-id="03dbb-215">Before you can delete a vault used to protect a Production server, you must delete or unregister the server from the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-215">Before you can delete a vault used to protect a Production server, you must delete or unregister the server from the vault.</span></span>

<span data-ttu-id="03dbb-216">To delete the Production server associated with the vault:</span><span class="sxs-lookup"><span data-stu-id="03dbb-216">To delete the Production server associated with the vault:</span></span>

1. <span data-ttu-id="03dbb-217">In the Azure portal, open the vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-217">In the Azure portal, open the vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span></span>

    ![open Production Servers blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-production-server.png)

    <span data-ttu-id="03dbb-219">The **Production Servers** blade opens and lists all Production servers in the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-219">The **Production Servers** blade opens and lists all Production servers in the vault.</span></span>

    ![list of Production Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/list-of-production-servers.png)
2. <span data-ttu-id="03dbb-221">On the **Production Servers** blade, right-click on the server, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-221">On the **Production Servers** blade, right-click on the server, and click **Delete**.</span></span>

    ![<span data-ttu-id="03dbb-222">delete production server</span><span class="sxs-lookup"><span data-stu-id="03dbb-222">delete production server</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    <span data-ttu-id="03dbb-223">The **Delete** blade opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-223">The **Delete** blade opens.</span></span>

    ![<span data-ttu-id="03dbb-224">delete production server</span><span class="sxs-lookup"><span data-stu-id="03dbb-224">delete production server</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/delete-blade.png)
3. <span data-ttu-id="03dbb-225">On the **Delete** blade, confirm the server name, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-225">On the **Delete** blade, confirm the server name, and click **Delete**.</span></span> <span data-ttu-id="03dbb-226">You must correctly name the server, to activate the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="03dbb-226">You must correctly name the server, to activate the **Delete** button.</span></span>

    <span data-ttu-id="03dbb-227">Once the vault is deleted, you receive a message stating the vault has been deleted.</span><span class="sxs-lookup"><span data-stu-id="03dbb-227">Once the vault is deleted, you receive a message stating the vault has been deleted.</span></span> <span data-ttu-id="03dbb-228">After deleting all servers in the vault, scroll back to the Essentials pane in the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="03dbb-228">After deleting all servers in the vault, scroll back to the Essentials pane in the vault dashboard.</span></span>
4. <span data-ttu-id="03dbb-229">In the vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-229">In the vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="03dbb-230">On the vault toolbar, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-230">On the vault toolbar, click **Delete**.</span></span>
5. <span data-ttu-id="03dbb-231">To verify that you want to delete the vault, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-231">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="03dbb-232">The vault is deleted and the portal returns to the **New** service menu.</span><span class="sxs-lookup"><span data-stu-id="03dbb-232">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-backup-vault-in-classic-portal"></a><span data-ttu-id="03dbb-233">Delete a backup vault in classic portal</span><span class="sxs-lookup"><span data-stu-id="03dbb-233">Delete a backup vault in classic portal</span></span>
<span data-ttu-id="03dbb-234">The following instructions are for deleting a Backup vault in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="03dbb-234">The following instructions are for deleting a Backup vault in the classic portal.</span></span> <span data-ttu-id="03dbb-235">Before you can delete the Backup vault, you must delete the recovery points, or backed up items, and remove the registered servers.</span><span class="sxs-lookup"><span data-stu-id="03dbb-235">Before you can delete the Backup vault, you must delete the recovery points, or backed up items, and remove the registered servers.</span></span> <span data-ttu-id="03dbb-236">The registered servers are the Windows Server, workstation, or virtual machines that were registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-236">The registered servers are the Windows Server, workstation, or virtual machines that were registered to the vault.</span></span>

1. <span data-ttu-id="03dbb-237">Open the [Classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="03dbb-237">Open the [Classic portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="03dbb-238">From the list of backup vaults, select the vault you want to delete.</span><span class="sxs-lookup"><span data-stu-id="03dbb-238">From the list of backup vaults, select the vault you want to delete.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    <span data-ttu-id="03dbb-240">The vault dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-240">The vault dashboard opens.</span></span> <span data-ttu-id="03dbb-241">Look at the number of Windows Servers and/or Azure virtual machines associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-241">Look at the number of Windows Servers and/or Azure virtual machines associated with the vault.</span></span> <span data-ttu-id="03dbb-242">Also, look at the total storage consumed in Azure.</span><span class="sxs-lookup"><span data-stu-id="03dbb-242">Also, look at the total storage consumed in Azure.</span></span> <span data-ttu-id="03dbb-243">Stop all backup jobs and delete all data before deleting the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-243">Stop all backup jobs and delete all data before deleting the vault.</span></span>

3. <span data-ttu-id="03dbb-244">Click the **Protected Items** tab, and then click **Stop Protection**</span><span class="sxs-lookup"><span data-stu-id="03dbb-244">Click the **Protected Items** tab, and then click **Stop Protection**</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    <span data-ttu-id="03dbb-246">The **Stop protection of 'your vault'** dialog appears.</span><span class="sxs-lookup"><span data-stu-id="03dbb-246">The **Stop protection of 'your vault'** dialog appears.</span></span>
4. <span data-ttu-id="03dbb-247">In the **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/checkmark.png).</span><span class="sxs-lookup"><span data-stu-id="03dbb-247">In the **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/checkmark.png).</span></span> <br/>
    <span data-ttu-id="03dbb-248">Optionally, you can choose a reason for stopping protection, and provide a comment.</span><span class="sxs-lookup"><span data-stu-id="03dbb-248">Optionally, you can choose a reason for stopping protection, and provide a comment.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    <span data-ttu-id="03dbb-250">After deleting the items in the vault, the vault will be empty.</span><span class="sxs-lookup"><span data-stu-id="03dbb-250">After deleting the items in the vault, the vault will be empty.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. <span data-ttu-id="03dbb-252">In the list of tabs, click **Registered Items**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-252">In the list of tabs, click **Registered Items**.</span></span> <span data-ttu-id="03dbb-253">The **Type** drop-down menu, enables you to choose the type of server registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-253">The **Type** drop-down menu, enables you to choose the type of server registered to the vault.</span></span> <span data-ttu-id="03dbb-254">The type can be Windows Server or Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="03dbb-254">The type can be Windows Server or Azure Virtual Machine.</span></span> <span data-ttu-id="03dbb-255">In the following example, select the virtual machine registered to the vault, and click **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-255">In the following example, select the virtual machine registered to the vault, and click **Unregister**.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-unregister.png)

  <span data-ttu-id="03dbb-257">If you want to delete the registration for a Windows Server, from the **Type** drop-down menu, select **Windows Server**, click ![checkmark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/checkmark.png) to refresh the screen, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-257">If you want to delete the registration for a Windows Server, from the **Type** drop-down menu, select **Windows Server**, click ![checkmark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/checkmark.png) to refresh the screen, and then click **Delete**.</span></span> <br/>

  ![select Windows Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/select-windows-server.png)

6. <span data-ttu-id="03dbb-259">In the list of tabs, click **Dashboard** to open that tab. Verify there are no registered servers or Azure virtual machines protected in the cloud.</span><span class="sxs-lookup"><span data-stu-id="03dbb-259">In the list of tabs, click **Dashboard** to open that tab. Verify there are no registered servers or Azure virtual machines protected in the cloud.</span></span> <span data-ttu-id="03dbb-260">Also, verify there is no data in storage.</span><span class="sxs-lookup"><span data-stu-id="03dbb-260">Also, verify there is no data in storage.</span></span> <span data-ttu-id="03dbb-261">Click **Delete** to delete the vault.</span><span class="sxs-lookup"><span data-stu-id="03dbb-261">Click **Delete** to delete the vault.</span></span>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    <span data-ttu-id="03dbb-263">The Delete Backup vault confirmation screen opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-263">The Delete Backup vault confirmation screen opens.</span></span> <span data-ttu-id="03dbb-264">Select an option why you're deleting the vault, and click</span><span class="sxs-lookup"><span data-stu-id="03dbb-264">Select an option why you're deleting the vault, and click</span></span> ![checkmark](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/checkmark.png)<span data-ttu-id="03dbb-266">.</span><span class="sxs-lookup"><span data-stu-id="03dbb-266">.</span></span> <br/>

    ![delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    <span data-ttu-id="03dbb-268">The vault is deleted, and you return to the classic portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="03dbb-268">The vault is deleted, and you return to the classic portal dashboard.</span></span>

### <a name="find-the-backup-management-servers-registered-to-the-vault"></a><span data-ttu-id="03dbb-269">Find the Backup Management servers registered to the vault</span><span class="sxs-lookup"><span data-stu-id="03dbb-269">Find the Backup Management servers registered to the vault</span></span>
<span data-ttu-id="03dbb-270">If you have multiple servers registered to a vault, it can be difficult to remember them.</span><span class="sxs-lookup"><span data-stu-id="03dbb-270">If you have multiple servers registered to a vault, it can be difficult to remember them.</span></span> <span data-ttu-id="03dbb-271">To see the servers registered to the vault, and delete them:</span><span class="sxs-lookup"><span data-stu-id="03dbb-271">To see the servers registered to the vault, and delete them:</span></span>

1. <span data-ttu-id="03dbb-272">Open the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="03dbb-272">Open the vault dashboard.</span></span>
2. <span data-ttu-id="03dbb-273">In the **Essentials** pane, click **Settings** to open that blade.</span><span class="sxs-lookup"><span data-stu-id="03dbb-273">In the **Essentials** pane, click **Settings** to open that blade.</span></span>

    ![open settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. <span data-ttu-id="03dbb-275">On the **Settings blade**, click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-275">On the **Settings blade**, click **Backup Infrastructure**.</span></span>
4. <span data-ttu-id="03dbb-276">On the **Backup Infrastructure** blade, click **Backup Management Servers**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-276">On the **Backup Infrastructure** blade, click **Backup Management Servers**.</span></span> <span data-ttu-id="03dbb-277">The Backup Management Servers blade opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-277">The Backup Management Servers blade opens.</span></span>

    ![list of backup management servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. <span data-ttu-id="03dbb-279">To delete a server from the list, right-click the name of the server and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-279">To delete a server from the list, right-click the name of the server and then click **Delete**.</span></span>
    <span data-ttu-id="03dbb-280">The **Delete** blade opens.</span><span class="sxs-lookup"><span data-stu-id="03dbb-280">The **Delete** blade opens.</span></span>
6. <span data-ttu-id="03dbb-281">On the **Delete** blade, provide the name of the server.</span><span class="sxs-lookup"><span data-stu-id="03dbb-281">On the **Delete** blade, provide the name of the server.</span></span> <span data-ttu-id="03dbb-282">If it is a long name, you can copy and paste it from the list of Backup Management Servers.</span><span class="sxs-lookup"><span data-stu-id="03dbb-282">If it is a long name, you can copy and paste it from the list of Backup Management Servers.</span></span> <span data-ttu-id="03dbb-283">Then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="03dbb-283">Then click **Delete**.</span></span>  

































