---
title: Configure OS patching schedule for Linux-based HDInsight clusters -Azure | Microsoft Docs
description: Learn how to configure OS patching schedule for Linux-based HDInsight clusters.
services: hdinsight
documentationcenter: ''
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: ''
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 73f688377c59e378eac653d597df37ddaf19fa48
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552909"
---
# <a name="os-patching-for-hdinsight"></a><span data-ttu-id="5d8c7-103">OS patching for HDInsight</span><span class="sxs-lookup"><span data-stu-id="5d8c7-103">OS patching for HDInsight</span></span> 
<span data-ttu-id="5d8c7-104">As a managed Hadoop service, HDInsight takes care of patching the OS of the underlying VMs used by HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-104">As a managed Hadoop service, HDInsight takes care of patching the OS of the underlying VMs used by HDInsight clusters.</span></span> <span data-ttu-id="5d8c7-105">As of August 1, 2016, we have changed the guest OS patching policy for Linux-based HDInsight clusters (version 3.4 or greater).</span><span class="sxs-lookup"><span data-stu-id="5d8c7-105">As of August 1, 2016, we have changed the guest OS patching policy for Linux-based HDInsight clusters (version 3.4 or greater).</span></span> <span data-ttu-id="5d8c7-106">The goal of the new policy is to significantly reduce the number of reboots due to patching.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-106">The goal of the new policy is to significantly reduce the number of reboots due to patching.</span></span> <span data-ttu-id="5d8c7-107">The new policy will continue to patch virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-107">The new policy will continue to patch virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span></span> <span data-ttu-id="5d8c7-108">However, any given VM will only reboot at most once every 30 days due to guest OS patching.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-108">However, any given VM will only reboot at most once every 30 days due to guest OS patching.</span></span> <span data-ttu-id="5d8c7-109">In addition, the first reboot for a newly created cluster will not happen sooner than 30 days from the cluster creation date.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-109">In addition, the first reboot for a newly created cluster will not happen sooner than 30 days from the cluster creation date.</span></span> <span data-ttu-id="5d8c7-110">Patches will be effective once the VMs are rebooted.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-110">Patches will be effective once the VMs are rebooted.</span></span>

## <a name="how-to-configure-the-os-patching-schedule-for-linux-based-hdinsight-clusters"></a><span data-ttu-id="5d8c7-111">How to configure the OS patching schedule for Linux-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="5d8c7-111">How to configure the OS patching schedule for Linux-based HDInsight clusters</span></span>
<span data-ttu-id="5d8c7-112">The virtual machines in an HDInsight cluster need to be rebooted occasionally so that important security patches can be installed.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-112">The virtual machines in an HDInsight cluster need to be rebooted occasionally so that important security patches can be installed.</span></span> <span data-ttu-id="5d8c7-113">As of August 1, 2016, new Linux-based HDInsight clusters (version 3.4 or greater,) are rebooted using the following schedule:</span><span class="sxs-lookup"><span data-stu-id="5d8c7-113">As of August 1, 2016, new Linux-based HDInsight clusters (version 3.4 or greater,) are rebooted using the following schedule:</span></span>

1. <span data-ttu-id="5d8c7-114">A virtual machine in the cluster can only reboot for patches at most, once within a 30-day period.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-114">A virtual machine in the cluster can only reboot for patches at most, once within a 30-day period.</span></span>
2. <span data-ttu-id="5d8c7-115">The reboot occurs starting at 12AM UTC.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-115">The reboot occurs starting at 12AM UTC.</span></span>
3. <span data-ttu-id="5d8c7-116">The reboot process is staggered across virtual machines in the cluster, so the cluster is still available during the reboot process.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-116">The reboot process is staggered across virtual machines in the cluster, so the cluster is still available during the reboot process.</span></span>
4. <span data-ttu-id="5d8c7-117">The first reboot for a newly created cluster will not happen sooner than 30 days after the cluster creation date.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-117">The first reboot for a newly created cluster will not happen sooner than 30 days after the cluster creation date.</span></span>

<span data-ttu-id="5d8c7-118">Using the script action described in this article, you can modify the OS patching schedule as follows:</span><span class="sxs-lookup"><span data-stu-id="5d8c7-118">Using the script action described in this article, you can modify the OS patching schedule as follows:</span></span>
1. <span data-ttu-id="5d8c7-119">Enable or disable automatic reboots</span><span class="sxs-lookup"><span data-stu-id="5d8c7-119">Enable or disable automatic reboots</span></span>
2. <span data-ttu-id="5d8c7-120">Set the frequency of reboots (days between reboots)</span><span class="sxs-lookup"><span data-stu-id="5d8c7-120">Set the frequency of reboots (days between reboots)</span></span>
3. <span data-ttu-id="5d8c7-121">Set the day of the week when a reboot occurs</span><span class="sxs-lookup"><span data-stu-id="5d8c7-121">Set the day of the week when a reboot occurs</span></span>

> [!NOTE]
> <span data-ttu-id="5d8c7-122">This script action will only work with Linux-based HDInsight clusters created after August 1st, 2016.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-122">This script action will only work with Linux-based HDInsight clusters created after August 1st, 2016.</span></span> <span data-ttu-id="5d8c7-123">Patches will be effective only when VMs are rebooted.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-123">Patches will be effective only when VMs are rebooted.</span></span> 
>

## <a name="how-to-use-the-script"></a><span data-ttu-id="5d8c7-124">How to use the script</span><span class="sxs-lookup"><span data-stu-id="5d8c7-124">How to use the script</span></span> 

<span data-ttu-id="5d8c7-125">When using this script requires the following information:</span><span class="sxs-lookup"><span data-stu-id="5d8c7-125">When using this script requires the following information:</span></span>
1. <span data-ttu-id="5d8c7-126">The script location: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight uses this URI to find and run the script on all the virtual machines in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-126">The script location: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight uses this URI to find and run the script on all the virtual machines in the cluster.</span></span>
  
2. <span data-ttu-id="5d8c7-127">The cluster node types that the script is applied to: headnode, workernode, zookeeper.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-127">The cluster node types that the script is applied to: headnode, workernode, zookeeper.</span></span> <span data-ttu-id="5d8c7-128">This script must be applied to all node types in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-128">This script must be applied to all node types in the cluster.</span></span> <span data-ttu-id="5d8c7-129">If it is not applied to a node type, then the virtual machines for that node type will continue to use the previous patching schedule.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-129">If it is not applied to a node type, then the virtual machines for that node type will continue to use the previous patching schedule.</span></span>


3.  <span data-ttu-id="5d8c7-130">Parameter: This script accepts three numeric parameters:</span><span class="sxs-lookup"><span data-stu-id="5d8c7-130">Parameter: This script accepts three numeric parameters:</span></span>

    | <span data-ttu-id="5d8c7-131">Parameter</span><span class="sxs-lookup"><span data-stu-id="5d8c7-131">Parameter</span></span> | <span data-ttu-id="5d8c7-132">Definition</span><span class="sxs-lookup"><span data-stu-id="5d8c7-132">Definition</span></span> |
    | --- | --- |
    | <span data-ttu-id="5d8c7-133">Enable/disable automatic reboots</span><span class="sxs-lookup"><span data-stu-id="5d8c7-133">Enable/disable automatic reboots</span></span> |<span data-ttu-id="5d8c7-134">0 or 1.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-134">0 or 1.</span></span> <span data-ttu-id="5d8c7-135">A value of 0 disables automatic reboots while 1 enables automatic reboots.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-135">A value of 0 disables automatic reboots while 1 enables automatic reboots.</span></span> |
    | <span data-ttu-id="5d8c7-136">Frequency</span><span class="sxs-lookup"><span data-stu-id="5d8c7-136">Frequency</span></span> |<span data-ttu-id="5d8c7-137">7 to 90 (inclusive).</span><span class="sxs-lookup"><span data-stu-id="5d8c7-137">7 to 90 (inclusive).</span></span> <span data-ttu-id="5d8c7-138">The number of days to wait before rebooting the virtual machines for patches that require a reboot.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-138">The number of days to wait before rebooting the virtual machines for patches that require a reboot.</span></span> |
    | <span data-ttu-id="5d8c7-139">Day of week</span><span class="sxs-lookup"><span data-stu-id="5d8c7-139">Day of week</span></span> |<span data-ttu-id="5d8c7-140">1 to 7 (inclusive).</span><span class="sxs-lookup"><span data-stu-id="5d8c7-140">1 to 7 (inclusive).</span></span> <span data-ttu-id="5d8c7-141">A value of 1 indicates the reboot should occur on a Monday, and 7 indicates a Sunday.For example, using parameters of 1 60 2 results in automatic reboots every 60 days (at most) on Tuesday.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-141">A value of 1 indicates the reboot should occur on a Monday, and 7 indicates a Sunday.For example, using parameters of 1 60 2 results in automatic reboots every 60 days (at most) on Tuesday.</span></span> |
    | <span data-ttu-id="5d8c7-142">Persistence</span><span class="sxs-lookup"><span data-stu-id="5d8c7-142">Persistence</span></span> |<span data-ttu-id="5d8c7-143">When applying a script action to an existing cluster, you can mark the script as persisted.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-143">When applying a script action to an existing cluster, you can mark the script as persisted.</span></span> <span data-ttu-id="5d8c7-144">Persisted scripts are applied when new workernodes are added to the cluster through scaling operations.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-144">Persisted scripts are applied when new workernodes are added to the cluster through scaling operations.</span></span> |

> [!NOTE]
> <span data-ttu-id="5d8c7-145">You must mark this script as persisted when applying to an existing cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-145">You must mark this script as persisted when applying to an existing cluster.</span></span> <span data-ttu-id="5d8c7-146">Otherwise, any new nodes created through scaling      operations will use the default patching schedule.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-146">Otherwise, any new nodes created through scaling      operations will use the default patching schedule.</span></span>
<span data-ttu-id="5d8c7-147">If you apply the script as part of the cluster creation process, it is persisted automatically.</span><span class="sxs-lookup"><span data-stu-id="5d8c7-147">If you apply the script as part of the cluster creation process, it is persisted automatically.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="5d8c7-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d8c7-148">Next steps</span></span>

<span data-ttu-id="5d8c7-149">For specific steps on using the script action, see the following sections in the [Customize Linuz-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md):</span><span class="sxs-lookup"><span data-stu-id="5d8c7-149">For specific steps on using the script action, see the following sections in the [Customize Linuz-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md):</span></span>

* [<span data-ttu-id="5d8c7-150">Use a script action during cluster creation</span><span class="sxs-lookup"><span data-stu-id="5d8c7-150">Use a script action during cluster creation</span></span>](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [<span data-ttu-id="5d8c7-151">Apply a script action to a running cluster</span><span class="sxs-lookup"><span data-stu-id="5d8c7-151">Apply a script action to a running cluster</span></span>](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
