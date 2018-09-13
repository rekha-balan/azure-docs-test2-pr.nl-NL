---
title: Use Azure Backup to replace your tape infrastructure | Microsoft Docs
description: Learn how Azure Backup provides tape-like semantics which enables you to backup and restore data in Azure
services: backup
documentationcenter: ''
author: trinadhk
manager: vijayts
editor: ''
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2955b30c5beb682ccfc1541cda7913a67b01140c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552306"
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="75fe5-103">Move your long-term storage from tape to the Azure cloud</span><span class="sxs-lookup"><span data-stu-id="75fe5-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="75fe5-104">Azure Backup and System Center Data Protection Manager customers can:</span><span class="sxs-lookup"><span data-stu-id="75fe5-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="75fe5-105">Back up data in schedules which best suit the organizational needs.</span><span class="sxs-lookup"><span data-stu-id="75fe5-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="75fe5-106">Retain the backup data for longer periods</span><span class="sxs-lookup"><span data-stu-id="75fe5-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="75fe5-107">Make Azure a part of their long-term retention needs (instead of tape).</span><span class="sxs-lookup"><span data-stu-id="75fe5-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="75fe5-108">This article explains how customers can enable backup and retention policies.</span><span class="sxs-lookup"><span data-stu-id="75fe5-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="75fe5-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span><span class="sxs-lookup"><span data-stu-id="75fe5-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="75fe5-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="75fe5-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="75fe5-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span><span class="sxs-lookup"><span data-stu-id="75fe5-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="75fe5-112">What is the Backup Schedule?</span><span class="sxs-lookup"><span data-stu-id="75fe5-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="75fe5-113">The backup schedule indicates the frequency of the backup operation.</span><span class="sxs-lookup"><span data-stu-id="75fe5-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="75fe5-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span><span class="sxs-lookup"><span data-stu-id="75fe5-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Daily Schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="75fe5-116">Customers can also schedule a weekly backup.</span><span class="sxs-lookup"><span data-stu-id="75fe5-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="75fe5-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span><span class="sxs-lookup"><span data-stu-id="75fe5-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Weekly Schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="75fe5-119">What is the Retention Policy?</span><span class="sxs-lookup"><span data-stu-id="75fe5-119">What is the Retention Policy?</span></span>
<span data-ttu-id="75fe5-120">The retention policy specifies the duration for which the backup must be stored.</span><span class="sxs-lookup"><span data-stu-id="75fe5-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="75fe5-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span><span class="sxs-lookup"><span data-stu-id="75fe5-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="75fe5-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span><span class="sxs-lookup"><span data-stu-id="75fe5-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="75fe5-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span><span class="sxs-lookup"><span data-stu-id="75fe5-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Retention Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="75fe5-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span><span class="sxs-lookup"><span data-stu-id="75fe5-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="75fe5-126">Example – Putting both together</span><span class="sxs-lookup"><span data-stu-id="75fe5-126">Example – Putting both together</span></span>
![Sample Screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="75fe5-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span><span class="sxs-lookup"><span data-stu-id="75fe5-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="75fe5-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span><span class="sxs-lookup"><span data-stu-id="75fe5-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="75fe5-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span><span class="sxs-lookup"><span data-stu-id="75fe5-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="75fe5-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span><span class="sxs-lookup"><span data-stu-id="75fe5-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="75fe5-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span><span class="sxs-lookup"><span data-stu-id="75fe5-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="75fe5-133">two points per day for seven days = 14 recovery points</span><span class="sxs-lookup"><span data-stu-id="75fe5-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="75fe5-134">two points per week for four weeks = 8 recovery points</span><span class="sxs-lookup"><span data-stu-id="75fe5-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="75fe5-135">two points per month for 12 months = 24 recovery points</span><span class="sxs-lookup"><span data-stu-id="75fe5-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="75fe5-136">one point per year per 10 years = 10 recovery points</span><span class="sxs-lookup"><span data-stu-id="75fe5-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="75fe5-137">The total number of recovery points is 56.</span><span class="sxs-lookup"><span data-stu-id="75fe5-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="75fe5-138">Azure backup doesn't have a restriction on number of recovery points.</span><span class="sxs-lookup"><span data-stu-id="75fe5-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="75fe5-139">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="75fe5-139">Advanced configuration</span></span>
<span data-ttu-id="75fe5-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span><span class="sxs-lookup"><span data-stu-id="75fe5-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modify](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="75fe5-142">Next Steps</span><span class="sxs-lookup"><span data-stu-id="75fe5-142">Next Steps</span></span>
<span data-ttu-id="75fe5-143">For more information about Azure Backup, see:</span><span class="sxs-lookup"><span data-stu-id="75fe5-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="75fe5-144">Introduction to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="75fe5-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="75fe5-145">Try Azure Backup</span><span class="sxs-lookup"><span data-stu-id="75fe5-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)





