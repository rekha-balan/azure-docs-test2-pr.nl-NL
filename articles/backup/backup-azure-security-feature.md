---
title: Security features to help protect hybrid backups that use Azure Backup | Microsoft Docs
description: Learn how to use security features in Azure Backup to make backups more secure
services: backup
documentationcenter: ''
author: JPallavi
manager: vijayts
editor: ''
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: pajosh
ms.openlocfilehash: 5938413a5aa33199e900f0af57245729b9d5dc03
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554193"
---
# <a name="security-features-to-help-protect-hybrid-backups-that-use-azure-backup"></a><span data-ttu-id="ae833-103">Security features to help protect hybrid backups that use Azure Backup</span><span class="sxs-lookup"><span data-stu-id="ae833-103">Security features to help protect hybrid backups that use Azure Backup</span></span>
<span data-ttu-id="ae833-104">Concerns about security issues, like malware, ransomware, and intrusion, are increasing.</span><span class="sxs-lookup"><span data-stu-id="ae833-104">Concerns about security issues, like malware, ransomware, and intrusion, are increasing.</span></span> <span data-ttu-id="ae833-105">These security issues can be costly, in terms of both money and data.</span><span class="sxs-lookup"><span data-stu-id="ae833-105">These security issues can be costly, in terms of both money and data.</span></span> <span data-ttu-id="ae833-106">To guard against such attacks, Azure Backup now provides security features to help protect hybrid backups.</span><span class="sxs-lookup"><span data-stu-id="ae833-106">To guard against such attacks, Azure Backup now provides security features to help protect hybrid backups.</span></span> <span data-ttu-id="ae833-107">This article covers how to enable and use these features, by using an Azure Recovery Services agent and Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="ae833-107">This article covers how to enable and use these features, by using an Azure Recovery Services agent and Azure Backup Server.</span></span> <span data-ttu-id="ae833-108">These features include:</span><span class="sxs-lookup"><span data-stu-id="ae833-108">These features include:</span></span>

- <span data-ttu-id="ae833-109">**Prevention**.</span><span class="sxs-lookup"><span data-stu-id="ae833-109">**Prevention**.</span></span> <span data-ttu-id="ae833-110">An additional layer of authentication is added whenever a critical operation like changing a passphrase is performed.</span><span class="sxs-lookup"><span data-stu-id="ae833-110">An additional layer of authentication is added whenever a critical operation like changing a passphrase is performed.</span></span> <span data-ttu-id="ae833-111">This validation is to ensure that such operations can be performed only by users who have valid Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="ae833-111">This validation is to ensure that such operations can be performed only by users who have valid Azure credentials.</span></span>
- <span data-ttu-id="ae833-112">**Alerting**.</span><span class="sxs-lookup"><span data-stu-id="ae833-112">**Alerting**.</span></span> <span data-ttu-id="ae833-113">An email notification is sent to the subscription admin whenever a critical operation like deleting backup data is performed.</span><span class="sxs-lookup"><span data-stu-id="ae833-113">An email notification is sent to the subscription admin whenever a critical operation like deleting backup data is performed.</span></span> <span data-ttu-id="ae833-114">This email ensures that the user is notified quickly about such actions.</span><span class="sxs-lookup"><span data-stu-id="ae833-114">This email ensures that the user is notified quickly about such actions.</span></span>
- <span data-ttu-id="ae833-115">**Recovery**.</span><span class="sxs-lookup"><span data-stu-id="ae833-115">**Recovery**.</span></span> <span data-ttu-id="ae833-116">Deleted backup data is retained for an additional 14 days from the date of the deletion.</span><span class="sxs-lookup"><span data-stu-id="ae833-116">Deleted backup data is retained for an additional 14 days from the date of the deletion.</span></span> <span data-ttu-id="ae833-117">This ensures recoverability of the data within a given time period, so there is no data loss even if an attack happens.</span><span class="sxs-lookup"><span data-stu-id="ae833-117">This ensures recoverability of the data within a given time period, so there is no data loss even if an attack happens.</span></span> <span data-ttu-id="ae833-118">Also, a greater number of minimum recovery points are maintained to guard against corrupt data.</span><span class="sxs-lookup"><span data-stu-id="ae833-118">Also, a greater number of minimum recovery points are maintained to guard against corrupt data.</span></span>

> [!NOTE]
> <span data-ttu-id="ae833-119">Security features should not be enabled if you are using infrastructure as a service (IaaS) VM backup.</span><span class="sxs-lookup"><span data-stu-id="ae833-119">Security features should not be enabled if you are using infrastructure as a service (IaaS) VM backup.</span></span> <span data-ttu-id="ae833-120">These features are not yet available for IaaS VM backup, so enabling them will not have any impact.</span><span class="sxs-lookup"><span data-stu-id="ae833-120">These features are not yet available for IaaS VM backup, so enabling them will not have any impact.</span></span> <span data-ttu-id="ae833-121">Security features should be enabled only if you are using:</span><span class="sxs-lookup"><span data-stu-id="ae833-121">Security features should be enabled only if you are using:</span></span> <br/>
>  * <span data-ttu-id="ae833-122">**Azure Backup agent**.</span><span class="sxs-lookup"><span data-stu-id="ae833-122">**Azure Backup agent**.</span></span> <span data-ttu-id="ae833-123">Minimum agent version 2.0.9052.</span><span class="sxs-lookup"><span data-stu-id="ae833-123">Minimum agent version 2.0.9052.</span></span> <span data-ttu-id="ae833-124">After you have enabled these features, you should upgrade to this agent version to perform critical operations.</span><span class="sxs-lookup"><span data-stu-id="ae833-124">After you have enabled these features, you should upgrade to this agent version to perform critical operations.</span></span> <br/>
>  * <span data-ttu-id="ae833-125">**Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="ae833-125">**Azure Backup Server**.</span></span> <span data-ttu-id="ae833-126">Minimum Azure Backup agent version 2.0.9052 with Azure Backup Server update 1.</span><span class="sxs-lookup"><span data-stu-id="ae833-126">Minimum Azure Backup agent version 2.0.9052 with Azure Backup Server update 1.</span></span> <br/>
>  * <span data-ttu-id="ae833-127">**System Center Data Protection Manager**.</span><span class="sxs-lookup"><span data-stu-id="ae833-127">**System Center Data Protection Manager**.</span></span> <span data-ttu-id="ae833-128">Minimum Azure Backup agent version 2.0.9052 with Data Protection Manager 2012 R2 UR12 or Data Protection Manager 2016 UR2.</span><span class="sxs-lookup"><span data-stu-id="ae833-128">Minimum Azure Backup agent version 2.0.9052 with Data Protection Manager 2012 R2 UR12 or Data Protection Manager 2016 UR2.</span></span> <br/> 


> [!NOTE]
> <span data-ttu-id="ae833-129">These features are available only for Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="ae833-129">These features are available only for Recovery Services vault.</span></span> <span data-ttu-id="ae833-130">All the newly created Recovery Services vaults have these features enabled by default.</span><span class="sxs-lookup"><span data-stu-id="ae833-130">All the newly created Recovery Services vaults have these features enabled by default.</span></span> <span data-ttu-id="ae833-131">For existing Recovery Services vaults, users enable these features by using the steps mentioned in the following section.</span><span class="sxs-lookup"><span data-stu-id="ae833-131">For existing Recovery Services vaults, users enable these features by using the steps mentioned in the following section.</span></span> <span data-ttu-id="ae833-132">After the features are enabled, they apply to all the Recovery Services agent computers, Azure Backup Server instances, and Data Protection Manager servers registered with the vault.</span><span class="sxs-lookup"><span data-stu-id="ae833-132">After the features are enabled, they apply to all the Recovery Services agent computers, Azure Backup Server instances, and Data Protection Manager servers registered with the vault.</span></span> <span data-ttu-id="ae833-133">Enabling this setting is a one-time action, and you cannot disable these features after enabling them.</span><span class="sxs-lookup"><span data-stu-id="ae833-133">Enabling this setting is a one-time action, and you cannot disable these features after enabling them.</span></span>
>

## <a name="enable-security-features"></a><span data-ttu-id="ae833-134">Enable security features</span><span class="sxs-lookup"><span data-stu-id="ae833-134">Enable security features</span></span>
<span data-ttu-id="ae833-135">If you are creating a Recovery Services vault, you can use all the security features.</span><span class="sxs-lookup"><span data-stu-id="ae833-135">If you are creating a Recovery Services vault, you can use all the security features.</span></span> <span data-ttu-id="ae833-136">If you are working with an existing vault, enable security features by following these steps:</span><span class="sxs-lookup"><span data-stu-id="ae833-136">If you are working with an existing vault, enable security features by following these steps:</span></span>

1. <span data-ttu-id="ae833-137">Sign in to the Azure portal by using your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="ae833-137">Sign in to the Azure portal by using your Azure credentials.</span></span>
2. <span data-ttu-id="ae833-138">Select **Browse**, and type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="ae833-138">Select **Browse**, and type **Recovery Services**.</span></span>

    ![Screenshot of Azure portal Browse option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="ae833-140">The list of recovery services vaults appears.</span><span class="sxs-lookup"><span data-stu-id="ae833-140">The list of recovery services vaults appears.</span></span> <span data-ttu-id="ae833-141">From this list, select a vault.</span><span class="sxs-lookup"><span data-stu-id="ae833-141">From this list, select a vault.</span></span> <span data-ttu-id="ae833-142">The selected vault dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="ae833-142">The selected vault dashboard opens.</span></span>
3. <span data-ttu-id="ae833-143">From the list of items that appears under the vault, under **Settings**, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ae833-143">From the list of items that appears under the vault, under **Settings**, click **Properties**.</span></span>

    ![Screenshot of Recovery Services vault options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-security-feature/vault-list-properties.png)
4. <span data-ttu-id="ae833-145">Under **Security Settings**, click **Update**.</span><span class="sxs-lookup"><span data-stu-id="ae833-145">Under **Security Settings**, click **Update**.</span></span>

    ![Screenshot of Recovery Services vault properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-security-feature/security-settings-update.png)

    <span data-ttu-id="ae833-147">The update link opens the **Security Settings** blade, which provides a summary of the features and lets you enable them.</span><span class="sxs-lookup"><span data-stu-id="ae833-147">The update link opens the **Security Settings** blade, which provides a summary of the features and lets you enable them.</span></span>
5. <span data-ttu-id="ae833-148">From the drop-down list **Have you configured Azure Multi-Factor Authentication?**, select a value to confirm if you have enabled [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ae833-148">From the drop-down list **Have you configured Azure Multi-Factor Authentication?**, select a value to confirm if you have enabled [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).</span></span> <span data-ttu-id="ae833-149">If it is enabled, you are asked to authenticate from another device (for example, a mobile phone) while signing in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae833-149">If it is enabled, you are asked to authenticate from another device (for example, a mobile phone) while signing in to the Azure portal.</span></span>

   <span data-ttu-id="ae833-150">When you perform critical operations in Backup, you have to enter a security PIN, available on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae833-150">When you perform critical operations in Backup, you have to enter a security PIN, available on the Azure portal.</span></span> <span data-ttu-id="ae833-151">Enabling Azure Multi-Factor Authentication adds a layer of security.</span><span class="sxs-lookup"><span data-stu-id="ae833-151">Enabling Azure Multi-Factor Authentication adds a layer of security.</span></span> <span data-ttu-id="ae833-152">Only authorized users with valid Azure credentials, and authenticated from a second device, can access the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae833-152">Only authorized users with valid Azure credentials, and authenticated from a second device, can access the Azure portal.</span></span>
6. <span data-ttu-id="ae833-153">To save security settings, select **Enable** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ae833-153">To save security settings, select **Enable** and click **Save**.</span></span> <span data-ttu-id="ae833-154">You can select **Enable** only after you select a value from the **Have you configured Azure Multi-Factor Authentication?** list in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ae833-154">You can select **Enable** only after you select a value from the **Have you configured Azure Multi-Factor Authentication?** list in the previous step.</span></span>

    ![Screenshot of security settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a><span data-ttu-id="ae833-156">Recover deleted backup data</span><span class="sxs-lookup"><span data-stu-id="ae833-156">Recover deleted backup data</span></span>
<span data-ttu-id="ae833-157">Backup retains deleted backup data for an additional 14 days, and does not delete it immediately if the **Stop backup with delete backup data** operation is performed.</span><span class="sxs-lookup"><span data-stu-id="ae833-157">Backup retains deleted backup data for an additional 14 days, and does not delete it immediately if the **Stop backup with delete backup data** operation is performed.</span></span> <span data-ttu-id="ae833-158">To restore this data in the 14-day period, take the following steps, depending on what you are using:</span><span class="sxs-lookup"><span data-stu-id="ae833-158">To restore this data in the 14-day period, take the following steps, depending on what you are using:</span></span>

<span data-ttu-id="ae833-159">For **Azure Recovery Services agent** users:</span><span class="sxs-lookup"><span data-stu-id="ae833-159">For **Azure Recovery Services agent** users:</span></span>

1. <span data-ttu-id="ae833-160">If the computer where backups were happening is still available, use [Recover data to the same machine](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) in Azure Recovery Services, to recover from all the old recovery points.</span><span class="sxs-lookup"><span data-stu-id="ae833-160">If the computer where backups were happening is still available, use [Recover data to the same machine](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) in Azure Recovery Services, to recover from all the old recovery points.</span></span>
2. <span data-ttu-id="ae833-161">If this computer is not available, use [Recover to an alternate machine](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) to use another Azure Recovery Services computer to get this data.</span><span class="sxs-lookup"><span data-stu-id="ae833-161">If this computer is not available, use [Recover to an alternate machine](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) to use another Azure Recovery Services computer to get this data.</span></span>

<span data-ttu-id="ae833-162">For **Azure Backup Server** users:</span><span class="sxs-lookup"><span data-stu-id="ae833-162">For **Azure Backup Server** users:</span></span>

1. <span data-ttu-id="ae833-163">If the server where backups were happening is still available, re-protect the deleted data sources, and use the **Recover Data** feature to recover from all the old recovery points.</span><span class="sxs-lookup"><span data-stu-id="ae833-163">If the server where backups were happening is still available, re-protect the deleted data sources, and use the **Recover Data** feature to recover from all the old recovery points.</span></span>
2. <span data-ttu-id="ae833-164">If this server is not available, use [Recover data from another Azure Backup Server](backup-azure-alternate-dpm-server.md#recover-data-from-another-azure-backup-server) to use another Azure Backup Server instance to get this data.</span><span class="sxs-lookup"><span data-stu-id="ae833-164">If this server is not available, use [Recover data from another Azure Backup Server](backup-azure-alternate-dpm-server.md#recover-data-from-another-azure-backup-server) to use another Azure Backup Server instance to get this data.</span></span>

<span data-ttu-id="ae833-165">For **Data Protection Manager** users:</span><span class="sxs-lookup"><span data-stu-id="ae833-165">For **Data Protection Manager** users:</span></span>

1. <span data-ttu-id="ae833-166">If the server where backups were happening is still available, re-protect the deleted data sources, and use the **Recover Data** feature to recover from all the old recovery points.</span><span class="sxs-lookup"><span data-stu-id="ae833-166">If the server where backups were happening is still available, re-protect the deleted data sources, and use the **Recover Data** feature to recover from all the old recovery points.</span></span>
2. <span data-ttu-id="ae833-167">If this server is not available, use [Add External DPM](backup-azure-alternate-dpm-server.md#recover-data-from-another-azure-backup-server) to use another Data Protection Manager server to get this data.</span><span class="sxs-lookup"><span data-stu-id="ae833-167">If this server is not available, use [Add External DPM](backup-azure-alternate-dpm-server.md#recover-data-from-another-azure-backup-server) to use another Data Protection Manager server to get this data.</span></span>

## <a name="prevent-attacks"></a><span data-ttu-id="ae833-168">Prevent attacks</span><span class="sxs-lookup"><span data-stu-id="ae833-168">Prevent attacks</span></span>
<span data-ttu-id="ae833-169">Checks have been added to make sure only valid users can perform various operations.</span><span class="sxs-lookup"><span data-stu-id="ae833-169">Checks have been added to make sure only valid users can perform various operations.</span></span> <span data-ttu-id="ae833-170">These include adding an extra layer of authentication, and maintaining a minimum retention range for recovery purposes.</span><span class="sxs-lookup"><span data-stu-id="ae833-170">These include adding an extra layer of authentication, and maintaining a minimum retention range for recovery purposes.</span></span>

### <a name="authentication-to-perform-critical-operations"></a><span data-ttu-id="ae833-171">Authentication to perform critical operations</span><span class="sxs-lookup"><span data-stu-id="ae833-171">Authentication to perform critical operations</span></span>
<span data-ttu-id="ae833-172">As part of adding an extra layer of authentication for critical operations, you are prompted to enter a security PIN when you perform **Stop Protection with Delete data** and **Change Passphrase** operations.</span><span class="sxs-lookup"><span data-stu-id="ae833-172">As part of adding an extra layer of authentication for critical operations, you are prompted to enter a security PIN when you perform **Stop Protection with Delete data** and **Change Passphrase** operations.</span></span>

<span data-ttu-id="ae833-173">To receive this PIN:</span><span class="sxs-lookup"><span data-stu-id="ae833-173">To receive this PIN:</span></span>

1. <span data-ttu-id="ae833-174">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae833-174">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="ae833-175">Browse to **Recovery Services vault** > **Settings** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ae833-175">Browse to **Recovery Services vault** > **Settings** > **Properties**.</span></span>
3. <span data-ttu-id="ae833-176">Under **Security PIN**, click **Generate**.</span><span class="sxs-lookup"><span data-stu-id="ae833-176">Under **Security PIN**, click **Generate**.</span></span> <span data-ttu-id="ae833-177">This opens a blade that contains the PIN to be entered in the Azure Recovery Services agent user interface.</span><span class="sxs-lookup"><span data-stu-id="ae833-177">This opens a blade that contains the PIN to be entered in the Azure Recovery Services agent user interface.</span></span>
    <span data-ttu-id="ae833-178">This PIN is valid for only five minutes, and it gets generated automatically after that period.</span><span class="sxs-lookup"><span data-stu-id="ae833-178">This PIN is valid for only five minutes, and it gets generated automatically after that period.</span></span>

### <a name="maintain-a-minimum-retention-range"></a><span data-ttu-id="ae833-179">Maintain a minimum retention range</span><span class="sxs-lookup"><span data-stu-id="ae833-179">Maintain a minimum retention range</span></span>
<span data-ttu-id="ae833-180">To ensure that there are always a valid number of recovery points available, the following checks have been added:</span><span class="sxs-lookup"><span data-stu-id="ae833-180">To ensure that there are always a valid number of recovery points available, the following checks have been added:</span></span>

- <span data-ttu-id="ae833-181">For daily retention, a minimum of **seven** days of retention should be done.</span><span class="sxs-lookup"><span data-stu-id="ae833-181">For daily retention, a minimum of **seven** days of retention should be done.</span></span>
- <span data-ttu-id="ae833-182">For weekly retention, a minimum of **four** weeks of retention should be done.</span><span class="sxs-lookup"><span data-stu-id="ae833-182">For weekly retention, a minimum of **four** weeks of retention should be done.</span></span>
- <span data-ttu-id="ae833-183">For monthly retention, a minimum of **three** months of retention should be done.</span><span class="sxs-lookup"><span data-stu-id="ae833-183">For monthly retention, a minimum of **three** months of retention should be done.</span></span>
- <span data-ttu-id="ae833-184">For yearly retention, a minimum of **one** year of retention should be done.</span><span class="sxs-lookup"><span data-stu-id="ae833-184">For yearly retention, a minimum of **one** year of retention should be done.</span></span>

## <a name="notifications-for-critical-operations"></a><span data-ttu-id="ae833-185">Notifications for critical operations</span><span class="sxs-lookup"><span data-stu-id="ae833-185">Notifications for critical operations</span></span>
<span data-ttu-id="ae833-186">Typically, when a critical operation is performed, the subscription admin is sent an email notification with details about the operation.</span><span class="sxs-lookup"><span data-stu-id="ae833-186">Typically, when a critical operation is performed, the subscription admin is sent an email notification with details about the operation.</span></span> <span data-ttu-id="ae833-187">You can configure additional email recipients for these notifications by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae833-187">You can configure additional email recipients for these notifications by using the Azure portal.</span></span>

<span data-ttu-id="ae833-188">The security features mentioned in this article provide defense mechanisms against targeted attacks.</span><span class="sxs-lookup"><span data-stu-id="ae833-188">The security features mentioned in this article provide defense mechanisms against targeted attacks.</span></span> <span data-ttu-id="ae833-189">More importantly, if an attack happens, these features give you the ability to recover your data.</span><span class="sxs-lookup"><span data-stu-id="ae833-189">More importantly, if an attack happens, these features give you the ability to recover your data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae833-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae833-190">Next steps</span></span>
* <span data-ttu-id="ae833-191">[Get started with Azure Recovery Services vault](backup-azure-vms-first-look-arm.md) to enable these features.</span><span class="sxs-lookup"><span data-stu-id="ae833-191">[Get started with Azure Recovery Services vault](backup-azure-vms-first-look-arm.md) to enable these features.</span></span>
* <span data-ttu-id="ae833-192">[Download the latest Azure Recovery Services agent](http://aka.ms/azurebackup_agent) to help protect Windows computers and guard your backup data against attacks.</span><span class="sxs-lookup"><span data-stu-id="ae833-192">[Download the latest Azure Recovery Services agent](http://aka.ms/azurebackup_agent) to help protect Windows computers and guard your backup data against attacks.</span></span>
* <span data-ttu-id="ae833-193">[Download the latest Azure Backup Server](https://aka.ms/latest_azurebackupserver) to help protect workloads and guard your backup data against attacks.</span><span class="sxs-lookup"><span data-stu-id="ae833-193">[Download the latest Azure Backup Server](https://aka.ms/latest_azurebackupserver) to help protect workloads and guard your backup data against attacks.</span></span>
* <span data-ttu-id="ae833-194">[Download UR12 for System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) or [download UR2 for System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) to help protect workloads and guard your backup data against attacks.</span><span class="sxs-lookup"><span data-stu-id="ae833-194">[Download UR12 for System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) or [download UR2 for System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) to help protect workloads and guard your backup data against attacks.</span></span>



