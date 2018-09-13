---
title: Set up replication settings for Azure Site Recovery| Microsoft Docs
description: Describes how to deploy Site Recovery to orchestrate replication, failover, and recovery of Hyper-V VMs in VMM clouds to Azure.
services: site-recovery
documentationcenter: ''
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/19/2017
ms.author: sutalasi
ms.openlocfilehash: a265d5c51f3eb8f12d78e082464b5a2d7971fb2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563344"
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="3cc19-103">Manage replication policy for VMware to Azure</span><span class="sxs-lookup"><span data-stu-id="3cc19-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="3cc19-104">Create a replication policy</span><span class="sxs-lookup"><span data-stu-id="3cc19-104">Create a replication policy</span></span>

1. <span data-ttu-id="3cc19-105">Select **Manage** > **Site Recovery Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="3cc19-106">Select **Replication policies** under **For VMware and Physical machines**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="3cc19-107">Select **+Replication policy**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-107">Select **+Replication policy**.</span></span>

    ![Create replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Createpolicy.png)

4. <span data-ttu-id="3cc19-109">Enter the policy name.</span><span class="sxs-lookup"><span data-stu-id="3cc19-109">Enter the policy name.</span></span>

5. <span data-ttu-id="3cc19-110">In **RPO threshold**, specify the RPO limit.</span><span class="sxs-lookup"><span data-stu-id="3cc19-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="3cc19-111">Alerts will be generated when continuous replication exceeds this limit.</span><span class="sxs-lookup"><span data-stu-id="3cc19-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="3cc19-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span><span class="sxs-lookup"><span data-stu-id="3cc19-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="3cc19-113">Protected machines can be recovered to any point within a retention window.</span><span class="sxs-lookup"><span data-stu-id="3cc19-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3cc19-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span><span class="sxs-lookup"><span data-stu-id="3cc19-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="3cc19-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span><span class="sxs-lookup"><span data-stu-id="3cc19-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3cc19-116">A replication policy for failback is automatically created.</span><span class="sxs-lookup"><span data-stu-id="3cc19-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="3cc19-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span><span class="sxs-lookup"><span data-stu-id="3cc19-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="3cc19-118">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-118">Click **OK**.</span></span> <span data-ttu-id="3cc19-119">The policy should be created in 30 to 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="3cc19-119">The policy should be created in 30 to 60 seconds.</span></span>

![Replication policy generation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="3cc19-121">Associate a configuration server with a replication policy</span><span class="sxs-lookup"><span data-stu-id="3cc19-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="3cc19-122">Choose the replication policy to which you want to associate the configuration server.</span><span class="sxs-lookup"><span data-stu-id="3cc19-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="3cc19-123">Click **Associate**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-123">Click **Associate**.</span></span>
<span data-ttu-id="3cc19-124">![Associate configuration server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="3cc19-124">![Associate configuration server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="3cc19-125">Select the configuration server from the list of servers.</span><span class="sxs-lookup"><span data-stu-id="3cc19-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="3cc19-126">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-126">Click **OK**.</span></span> <span data-ttu-id="3cc19-127">The configuration server should be associated in one to two minutes.</span><span class="sxs-lookup"><span data-stu-id="3cc19-127">The configuration server should be associated in one to two minutes.</span></span>

![Configuration server association](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.PNG)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="3cc19-129">Edit a replication policy</span><span class="sxs-lookup"><span data-stu-id="3cc19-129">Edit a replication policy</span></span>
1. <span data-ttu-id="3cc19-130">Choose the replication policy for which you want to edit replication settings.</span><span class="sxs-lookup"><span data-stu-id="3cc19-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="3cc19-131">![Edit replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Select-Policy.PNG)</span><span class="sxs-lookup"><span data-stu-id="3cc19-131">![Edit replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Select-Policy.PNG)</span></span>

2. <span data-ttu-id="3cc19-132">Click **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="3cc19-133">![Edit replication policy settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Edit-policy.PNG)</span><span class="sxs-lookup"><span data-stu-id="3cc19-133">![Edit replication policy settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Edit-policy.PNG)</span></span>

3. <span data-ttu-id="3cc19-134">Change the settings based on your need.</span><span class="sxs-lookup"><span data-stu-id="3cc19-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="3cc19-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-135">Click **Save**.</span></span> <span data-ttu-id="3cc19-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span><span class="sxs-lookup"><span data-stu-id="3cc19-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Save replication policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-setup-replication-settings-vmware/Save-Policy.PNG)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="3cc19-138">Dissociate a configuration server from a replication policy</span><span class="sxs-lookup"><span data-stu-id="3cc19-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="3cc19-139">Choose the replication policy to which you want to associate the configuration server.</span><span class="sxs-lookup"><span data-stu-id="3cc19-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="3cc19-140">Click **Dissociate**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="3cc19-141">Select the configuration server from the list of servers.</span><span class="sxs-lookup"><span data-stu-id="3cc19-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="3cc19-142">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-142">Click **OK**.</span></span> <span data-ttu-id="3cc19-143">The configuration server should be dissociated in one to two minutes.</span><span class="sxs-lookup"><span data-stu-id="3cc19-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3cc19-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span><span class="sxs-lookup"><span data-stu-id="3cc19-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="3cc19-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span><span class="sxs-lookup"><span data-stu-id="3cc19-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="3cc19-146">Delete a replication policy</span><span class="sxs-lookup"><span data-stu-id="3cc19-146">Delete a replication policy</span></span>

1. <span data-ttu-id="3cc19-147">Choose the replication policy that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="3cc19-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="3cc19-148">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3cc19-148">Click **Delete**.</span></span> <span data-ttu-id="3cc19-149">The policy should be deleted in 30 to 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="3cc19-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3cc19-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span><span class="sxs-lookup"><span data-stu-id="3cc19-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="3cc19-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span><span class="sxs-lookup"><span data-stu-id="3cc19-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>







