---
title: Troubleshoot System Center Data Protection Manager with Azure Backup
description: Troubleshoot issues in System Center Data Protection Manager.
services: backup
author: adigan
manager: shreeshd
ms.service: backup
ms.topic: conceptual
ms.date: 11/24/2017
ms.author: adigan
ms.openlocfilehash: d3776df8184523999433059e95bc72e1d3abb1c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856116"
---
# <a name="troubleshoot-system-center-data-protection-manager"></a><span data-ttu-id="535d7-103">Troubleshoot System Center Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="535d7-103">Troubleshoot System Center Data Protection Manager</span></span>

<span data-ttu-id="535d7-104">This article describes solutions for issues that you might encounter while using Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="535d7-104">This article describes solutions for issues that you might encounter while using Data Protection Manager.</span></span>

<span data-ttu-id="535d7-105">For the latest release notes for System Center Data Protection Manager, see the [System Center documentation](https://docs.microsoft.com/system-center/dpm/dpm-release-notes?view=sc-dpm-2016).</span><span class="sxs-lookup"><span data-stu-id="535d7-105">For the latest release notes for System Center Data Protection Manager, see the [System Center documentation](https://docs.microsoft.com/system-center/dpm/dpm-release-notes?view=sc-dpm-2016).</span></span> <span data-ttu-id="535d7-106">You can learn more about support for Data Protection Manager in [this matrix](https://docs.microsoft.com/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2016).</span><span class="sxs-lookup"><span data-stu-id="535d7-106">You can learn more about support for Data Protection Manager in [this matrix](https://docs.microsoft.com/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2016).</span></span>


## <a name="error-replica-is-inconsistent"></a><span data-ttu-id="535d7-107">Error: Replica is inconsistent</span><span class="sxs-lookup"><span data-stu-id="535d7-107">Error: Replica is inconsistent</span></span>

<span data-ttu-id="535d7-108">A replica can be inconsistent for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="535d7-108">A replica can be inconsistent for the following reasons:</span></span>
- <span data-ttu-id="535d7-109">The replica creation job fails.</span><span class="sxs-lookup"><span data-stu-id="535d7-109">The replica creation job fails.</span></span>
- <span data-ttu-id="535d7-110">There are issues with the change journal.</span><span class="sxs-lookup"><span data-stu-id="535d7-110">There are issues with the change journal.</span></span>
- <span data-ttu-id="535d7-111">The volume level filter bitmap contains errors.</span><span class="sxs-lookup"><span data-stu-id="535d7-111">The volume level filter bitmap contains errors.</span></span>
- <span data-ttu-id="535d7-112">The source machine shuts down unexpectedly.</span><span class="sxs-lookup"><span data-stu-id="535d7-112">The source machine shuts down unexpectedly.</span></span>
- <span data-ttu-id="535d7-113">The synchronization log overflows.</span><span class="sxs-lookup"><span data-stu-id="535d7-113">The synchronization log overflows.</span></span>
- <span data-ttu-id="535d7-114">The replica is truly inconsistent.</span><span class="sxs-lookup"><span data-stu-id="535d7-114">The replica is truly inconsistent.</span></span>

<span data-ttu-id="535d7-115">To resolve this issue, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="535d7-115">To resolve this issue, perform the following actions:</span></span>
- <span data-ttu-id="535d7-116">To remove the inconsistent status, run the consistency check manually, or schedule a daily consistency check.</span><span class="sxs-lookup"><span data-stu-id="535d7-116">To remove the inconsistent status, run the consistency check manually, or schedule a daily consistency check.</span></span>
- <span data-ttu-id="535d7-117">Ensure that you're using the latest version of Microsoft Azure Backup Server and Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="535d7-117">Ensure that you're using the latest version of Microsoft Azure Backup Server and Data Protection Manager.</span></span>
- <span data-ttu-id="535d7-118">Ensure that the **Automatic Consistency** setting is enabled.</span><span class="sxs-lookup"><span data-stu-id="535d7-118">Ensure that the **Automatic Consistency** setting is enabled.</span></span>
- <span data-ttu-id="535d7-119">Try to restart the services from the command prompt.</span><span class="sxs-lookup"><span data-stu-id="535d7-119">Try to restart the services from the command prompt.</span></span> <span data-ttu-id="535d7-120">Use the `net stop dpmra` command followed by `net start dpmra`.</span><span class="sxs-lookup"><span data-stu-id="535d7-120">Use the `net stop dpmra` command followed by `net start dpmra`.</span></span>
- <span data-ttu-id="535d7-121">Ensure that you're meeting the network connectivity and bandwidth requirements.</span><span class="sxs-lookup"><span data-stu-id="535d7-121">Ensure that you're meeting the network connectivity and bandwidth requirements.</span></span>
- <span data-ttu-id="535d7-122">Check if the source machine was shut down unexpectedly.</span><span class="sxs-lookup"><span data-stu-id="535d7-122">Check if the source machine was shut down unexpectedly.</span></span>
- <span data-ttu-id="535d7-123">Ensure that the disk is healthy and that there's enough space for the replica.</span><span class="sxs-lookup"><span data-stu-id="535d7-123">Ensure that the disk is healthy and that there's enough space for the replica.</span></span>
- <span data-ttu-id="535d7-124">Ensure that there are no duplicate backup jobs that are running concurrently.</span><span class="sxs-lookup"><span data-stu-id="535d7-124">Ensure that there are no duplicate backup jobs that are running concurrently.</span></span>

## <a name="error-online-recovery-point-creation-failed"></a><span data-ttu-id="535d7-125">Error: Online recovery point creation failed</span><span class="sxs-lookup"><span data-stu-id="535d7-125">Error: Online recovery point creation failed</span></span>

<span data-ttu-id="535d7-126">To resolve this issue, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="535d7-126">To resolve this issue, perform the following actions:</span></span>
- <span data-ttu-id="535d7-127">Ensure that you're using the latest version of the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="535d7-127">Ensure that you're using the latest version of the Azure Backup agent.</span></span>
- <span data-ttu-id="535d7-128">Try to manually create a recovery point in the protection task area.</span><span class="sxs-lookup"><span data-stu-id="535d7-128">Try to manually create a recovery point in the protection task area.</span></span>
- <span data-ttu-id="535d7-129">Ensure that you run a consistency check on the data source.</span><span class="sxs-lookup"><span data-stu-id="535d7-129">Ensure that you run a consistency check on the data source.</span></span>
- <span data-ttu-id="535d7-130">Ensure that you're meeting the network connectivity and bandwidth requirements.</span><span class="sxs-lookup"><span data-stu-id="535d7-130">Ensure that you're meeting the network connectivity and bandwidth requirements.</span></span>
- <span data-ttu-id="535d7-131">When the replica data is in an inconsistent state, create a disk recovery point of this data source.</span><span class="sxs-lookup"><span data-stu-id="535d7-131">When the replica data is in an inconsistent state, create a disk recovery point of this data source.</span></span>
- <span data-ttu-id="535d7-132">Ensure that the replica is present and not missing.</span><span class="sxs-lookup"><span data-stu-id="535d7-132">Ensure that the replica is present and not missing.</span></span>
- <span data-ttu-id="535d7-133">Ensure that the replica has sufficient space to create the update sequence number (USN) journal.</span><span class="sxs-lookup"><span data-stu-id="535d7-133">Ensure that the replica has sufficient space to create the update sequence number (USN) journal.</span></span>

## <a name="error-unable-to-configure-protection"></a><span data-ttu-id="535d7-134">Error: Unable to configure protection</span><span class="sxs-lookup"><span data-stu-id="535d7-134">Error: Unable to configure protection</span></span>

<span data-ttu-id="535d7-135">This error occurs when the Data Protection Manager server can't contact the protected server.</span><span class="sxs-lookup"><span data-stu-id="535d7-135">This error occurs when the Data Protection Manager server can't contact the protected server.</span></span> 

<span data-ttu-id="535d7-136">To resolve this issue, perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="535d7-136">To resolve this issue, perform the following actions:</span></span>
- <span data-ttu-id="535d7-137">Ensure that you're using the latest version of the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="535d7-137">Ensure that you're using the latest version of the Azure Backup agent.</span></span>
- <span data-ttu-id="535d7-138">Ensure that there's connectivity (network/firewall/proxy) between your Data Protection Manager server and the protected server.</span><span class="sxs-lookup"><span data-stu-id="535d7-138">Ensure that there's connectivity (network/firewall/proxy) between your Data Protection Manager server and the protected server.</span></span>
- <span data-ttu-id="535d7-139">If you're protecting a SQL server, ensure that the **Login Properties** > **NT AUTHORITY\SYSTEM** property shows the **sysadmin** setting enabled.</span><span class="sxs-lookup"><span data-stu-id="535d7-139">If you're protecting a SQL server, ensure that the **Login Properties** > **NT AUTHORITY\SYSTEM** property shows the **sysadmin** setting enabled.</span></span>

## <a name="error-server-not-registered-as-specified-in-vault-credential-file"></a><span data-ttu-id="535d7-140">Error: Server not registered as specified in vault credential file</span><span class="sxs-lookup"><span data-stu-id="535d7-140">Error: Server not registered as specified in vault credential file</span></span>

<span data-ttu-id="535d7-141">This error occurs during the recovery process for Data Protection Manager/Azure Backup server data.</span><span class="sxs-lookup"><span data-stu-id="535d7-141">This error occurs during the recovery process for Data Protection Manager/Azure Backup server data.</span></span> <span data-ttu-id="535d7-142">The vault credential file that's used in the recovery process doesn't belong to the Recovery Services vault for the Data Protection Manager/Azure Backup server.</span><span class="sxs-lookup"><span data-stu-id="535d7-142">The vault credential file that's used in the recovery process doesn't belong to the Recovery Services vault for the Data Protection Manager/Azure Backup server.</span></span>

<span data-ttu-id="535d7-143">To resolve this issue, perform these steps:</span><span class="sxs-lookup"><span data-stu-id="535d7-143">To resolve this issue, perform these steps:</span></span>
1. <span data-ttu-id="535d7-144">Download the vault credential file from the Recovery Services vault to which the Data Protection Manager/Azure Backup server is registered.</span><span class="sxs-lookup"><span data-stu-id="535d7-144">Download the vault credential file from the Recovery Services vault to which the Data Protection Manager/Azure Backup server is registered.</span></span>
2. <span data-ttu-id="535d7-145">Try to register the server with the vault by using the most recently downloaded vault credential file.</span><span class="sxs-lookup"><span data-stu-id="535d7-145">Try to register the server with the vault by using the most recently downloaded vault credential file.</span></span>

## <a name="error-no-recoverable-data-or-selected-server-not-a-data-protection-manager-server"></a><span data-ttu-id="535d7-146">Error: No recoverable data or selected server not a Data Protection Manager server</span><span class="sxs-lookup"><span data-stu-id="535d7-146">Error: No recoverable data or selected server not a Data Protection Manager server</span></span>

<span data-ttu-id="535d7-147">This error occurs for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="535d7-147">This error occurs for the following reasons:</span></span>
- <span data-ttu-id="535d7-148">No other Data Protection Manager/Azure Backup servers are registered to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="535d7-148">No other Data Protection Manager/Azure Backup servers are registered to the Recovery Services vault.</span></span>
- <span data-ttu-id="535d7-149">The servers haven't yet uploaded the metadata.</span><span class="sxs-lookup"><span data-stu-id="535d7-149">The servers haven't yet uploaded the metadata.</span></span>
- <span data-ttu-id="535d7-150">The selected server isn't a Data Protection Manager/Azure Backup server.</span><span class="sxs-lookup"><span data-stu-id="535d7-150">The selected server isn't a Data Protection Manager/Azure Backup server.</span></span>

<span data-ttu-id="535d7-151">When other Data Protection Manager/Azure Backup servers are registered to the Recovery Services vault, perform these steps to resolve the issue:</span><span class="sxs-lookup"><span data-stu-id="535d7-151">When other Data Protection Manager/Azure Backup servers are registered to the Recovery Services vault, perform these steps to resolve the issue:</span></span>
1. <span data-ttu-id="535d7-152">Ensure that the latest Azure Backup agent is installed.</span><span class="sxs-lookup"><span data-stu-id="535d7-152">Ensure that the latest Azure Backup agent is installed.</span></span>
2. <span data-ttu-id="535d7-153">After you ensure that the latest agent is installed, wait one day before you start the recovery process.</span><span class="sxs-lookup"><span data-stu-id="535d7-153">After you ensure that the latest agent is installed, wait one day before you start the recovery process.</span></span> <span data-ttu-id="535d7-154">The nightly backup job uploads the metadata for all of the protected backups to the cloud.</span><span class="sxs-lookup"><span data-stu-id="535d7-154">The nightly backup job uploads the metadata for all of the protected backups to the cloud.</span></span> <span data-ttu-id="535d7-155">The backup data is then available for recovery.</span><span class="sxs-lookup"><span data-stu-id="535d7-155">The backup data is then available for recovery.</span></span>

## <a name="error-provided-encryption-passphrase-doesnt-match-passphrase-for-server"></a><span data-ttu-id="535d7-156">Error: Provided encryption passphrase doesn't match passphrase for server</span><span class="sxs-lookup"><span data-stu-id="535d7-156">Error: Provided encryption passphrase doesn't match passphrase for server</span></span>

<span data-ttu-id="535d7-157">This error occurs during the encryption process when recovering Data Protection Manager/Azure Backup server data.</span><span class="sxs-lookup"><span data-stu-id="535d7-157">This error occurs during the encryption process when recovering Data Protection Manager/Azure Backup server data.</span></span> <span data-ttu-id="535d7-158">The encryption passphrase that's used in the recovery process doesn't match the server's encryption passphrase.</span><span class="sxs-lookup"><span data-stu-id="535d7-158">The encryption passphrase that's used in the recovery process doesn't match the server's encryption passphrase.</span></span> <span data-ttu-id="535d7-159">As a result, the agent can't decrypt the data and the recovery fails.</span><span class="sxs-lookup"><span data-stu-id="535d7-159">As a result, the agent can't decrypt the data and the recovery fails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="535d7-160">If you forget or lose the encryption passphrase, there are no other methods for recovering the data.</span><span class="sxs-lookup"><span data-stu-id="535d7-160">If you forget or lose the encryption passphrase, there are no other methods for recovering the data.</span></span> <span data-ttu-id="535d7-161">The only option is to regenerate the passphrase.</span><span class="sxs-lookup"><span data-stu-id="535d7-161">The only option is to regenerate the passphrase.</span></span> <span data-ttu-id="535d7-162">Use the new passphrase to encrypt future backup data.</span><span class="sxs-lookup"><span data-stu-id="535d7-162">Use the new passphrase to encrypt future backup data.</span></span>
>
> <span data-ttu-id="535d7-163">When you're recovering data, always provide the same encryption passphrase that's associated with the Data Protection Manager/Azure Backup server.</span><span class="sxs-lookup"><span data-stu-id="535d7-163">When you're recovering data, always provide the same encryption passphrase that's associated with the Data Protection Manager/Azure Backup server.</span></span> 
>
