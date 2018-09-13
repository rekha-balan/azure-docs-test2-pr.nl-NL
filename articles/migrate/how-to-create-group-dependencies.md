---
title: Refine an assessment group with group dependency mapping in Azure Migrate | Microsoft Docs
description: Describes how to refine an assessment using group dependency mapping in the Azure Migrate service.
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 06/19/2018
ms.author: raynew
ms.openlocfilehash: 37c4ce8638c8f0481151449317d6cd387b61b256
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867659"
---
# <a name="refine-a-group-using-group-dependency-mapping"></a><span data-ttu-id="f65cd-103">Refine a group using group dependency mapping</span><span class="sxs-lookup"><span data-stu-id="f65cd-103">Refine a group using group dependency mapping</span></span>

<span data-ttu-id="f65cd-104">This article describes how to refine a group by visualizing dependencies of all machines in the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-104">This article describes how to refine a group by visualizing dependencies of all machines in the group.</span></span> <span data-ttu-id="f65cd-105">You typically use this method when you want to refine membership for an existing group, by cross-checking group dependencies, before you run an assessment.</span><span class="sxs-lookup"><span data-stu-id="f65cd-105">You typically use this method when you want to refine membership for an existing group, by cross-checking group dependencies, before you run an assessment.</span></span> <span data-ttu-id="f65cd-106">Refining a group using dependency visualization can help you effectively plan your migration to Azure.You can discover all interdependent systems that need to migrate together.</span><span class="sxs-lookup"><span data-stu-id="f65cd-106">Refining a group using dependency visualization can help you effectively plan your migration to Azure.You can discover all interdependent systems that need to migrate together.</span></span> <span data-ttu-id="f65cd-107">It helps you ensure that nothing is left behind and surprise outages do not occur when you are migrating to Azure.</span><span class="sxs-lookup"><span data-stu-id="f65cd-107">It helps you ensure that nothing is left behind and surprise outages do not occur when you are migrating to Azure.</span></span> 


> [!NOTE]
> <span data-ttu-id="f65cd-108">Groups for which you want to visualize dependencies shouldn't contain more than 10 machines.</span><span class="sxs-lookup"><span data-stu-id="f65cd-108">Groups for which you want to visualize dependencies shouldn't contain more than 10 machines.</span></span> <span data-ttu-id="f65cd-109">If you have more than 10 machines in the group, we recommend you to split it into smaller groups to leverage the dependency visualization functionality.</span><span class="sxs-lookup"><span data-stu-id="f65cd-109">If you have more than 10 machines in the group, we recommend you to split it into smaller groups to leverage the dependency visualization functionality.</span></span>


# <a name="prepare-the-group-for-dependency-visualization"></a><span data-ttu-id="f65cd-110">Prepare the group for dependency visualization</span><span class="sxs-lookup"><span data-stu-id="f65cd-110">Prepare the group for dependency visualization</span></span>
<span data-ttu-id="f65cd-111">To view dependencies of a group, you need to download and install agents on each on-premises machine that is part of the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-111">To view dependencies of a group, you need to download and install agents on each on-premises machine that is part of the group.</span></span> <span data-ttu-id="f65cd-112">In addition, if you have machines with no internet connectivity, you need to download and install [OMS gateway](../log-analytics/log-analytics-oms-gateway.md) on them.</span><span class="sxs-lookup"><span data-stu-id="f65cd-112">In addition, if you have machines with no internet connectivity, you need to download and install [OMS gateway](../log-analytics/log-analytics-oms-gateway.md) on them.</span></span>

### <a name="download-and-install-the-vm-agents"></a><span data-ttu-id="f65cd-113">Download and install the VM agents</span><span class="sxs-lookup"><span data-stu-id="f65cd-113">Download and install the VM agents</span></span>
1. <span data-ttu-id="f65cd-114">In **Overview**, click **Manage** > **Groups**, go to the required group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-114">In **Overview**, click **Manage** > **Groups**, go to the required group.</span></span>
2. <span data-ttu-id="f65cd-115">In the list of machines, in the **Dependency agent** column, click **Requires installation** to see instructions regarding how to download and install the agents.</span><span class="sxs-lookup"><span data-stu-id="f65cd-115">In the list of machines, in the **Dependency agent** column, click **Requires installation** to see instructions regarding how to download and install the agents.</span></span>
3. <span data-ttu-id="f65cd-116">On the **Dependencies** page, download and install the Microsoft Monitoring Agent (MMA), and the Dependency agent on each VM that is part of the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-116">On the **Dependencies** page, download and install the Microsoft Monitoring Agent (MMA), and the Dependency agent on each VM that is part of the group.</span></span>
4. <span data-ttu-id="f65cd-117">Copy the workspace ID and key.</span><span class="sxs-lookup"><span data-stu-id="f65cd-117">Copy the workspace ID and key.</span></span> <span data-ttu-id="f65cd-118">You need these when you install the MMA on the on-premises machines.</span><span class="sxs-lookup"><span data-stu-id="f65cd-118">You need these when you install the MMA on the on-premises machines.</span></span>

### <a name="install-the-mma"></a><span data-ttu-id="f65cd-119">Install the MMA</span><span class="sxs-lookup"><span data-stu-id="f65cd-119">Install the MMA</span></span>

<span data-ttu-id="f65cd-120">To install the agent on a Windows machine:</span><span class="sxs-lookup"><span data-stu-id="f65cd-120">To install the agent on a Windows machine:</span></span>

1. <span data-ttu-id="f65cd-121">Double-click the downloaded agent.</span><span class="sxs-lookup"><span data-stu-id="f65cd-121">Double-click the downloaded agent.</span></span>
2. <span data-ttu-id="f65cd-122">On the **Welcome** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f65cd-122">On the **Welcome** page, click **Next**.</span></span> <span data-ttu-id="f65cd-123">On the **License Terms** page, click **I Agree** to accept the license.</span><span class="sxs-lookup"><span data-stu-id="f65cd-123">On the **License Terms** page, click **I Agree** to accept the license.</span></span>
3. <span data-ttu-id="f65cd-124">In **Destination Folder**, keep or modify the default installation folder > **Next**.</span><span class="sxs-lookup"><span data-stu-id="f65cd-124">In **Destination Folder**, keep or modify the default installation folder > **Next**.</span></span> 
4. <span data-ttu-id="f65cd-125">In **Agent Setup Options**, select **Azure Log Analytics** > **Next**.</span><span class="sxs-lookup"><span data-stu-id="f65cd-125">In **Agent Setup Options**, select **Azure Log Analytics** > **Next**.</span></span> 
5. <span data-ttu-id="f65cd-126">Click **Add** to add a new Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="f65cd-126">Click **Add** to add a new Log Analytics workspace.</span></span> <span data-ttu-id="f65cd-127">Paste in the workspace ID and key that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="f65cd-127">Paste in the workspace ID and key that you copied from the portal.</span></span> <span data-ttu-id="f65cd-128">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f65cd-128">Click **Next**.</span></span>


<span data-ttu-id="f65cd-129">To install the agent on a Linux machine:</span><span class="sxs-lookup"><span data-stu-id="f65cd-129">To install the agent on a Linux machine:</span></span>

1. <span data-ttu-id="f65cd-130">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span><span class="sxs-lookup"><span data-stu-id="f65cd-130">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
2. <span data-ttu-id="f65cd-131">Install the bundle by using the --install argument.</span><span class="sxs-lookup"><span data-stu-id="f65cd-131">Install the bundle by using the --install argument.</span></span>

    ```sudo sh ./omsagent-<version>.universal.x64.sh --install -w <workspace id> -s <workspace key>```


### <a name="install-the-dependency-agent"></a><span data-ttu-id="f65cd-132">Install the Dependency agent</span><span class="sxs-lookup"><span data-stu-id="f65cd-132">Install the Dependency agent</span></span>
1. <span data-ttu-id="f65cd-133">To install the Dependency agent on a Windows machine, double-click the setup file and follow the wizard.</span><span class="sxs-lookup"><span data-stu-id="f65cd-133">To install the Dependency agent on a Windows machine, double-click the setup file and follow the wizard.</span></span>
2. <span data-ttu-id="f65cd-134">To install the Dependency agent on a Linux machine, install as root using the following command:</span><span class="sxs-lookup"><span data-stu-id="f65cd-134">To install the Dependency agent on a Linux machine, install as root using the following command:</span></span>

    ```sh InstallDependencyAgent-Linux64.bin```

<span data-ttu-id="f65cd-135">Learn more about the Dependency agent support for the [Windows](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) and [Linux](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) operating systems.</span><span class="sxs-lookup"><span data-stu-id="f65cd-135">Learn more about the Dependency agent support for the [Windows](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) and [Linux](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) operating systems.</span></span>

## <a name="refine-the-group-based-on-dependency-visualization"></a><span data-ttu-id="f65cd-136">Refine the group based on dependency visualization</span><span class="sxs-lookup"><span data-stu-id="f65cd-136">Refine the group based on dependency visualization</span></span>
<span data-ttu-id="f65cd-137">Once you have installed agents on all the machines of the group, you can visualize the dependencies of the group and refine it by following the below steps.</span><span class="sxs-lookup"><span data-stu-id="f65cd-137">Once you have installed agents on all the machines of the group, you can visualize the dependencies of the group and refine it by following the below steps.</span></span>

1. <span data-ttu-id="f65cd-138">In the Azure Migrate project, under **Manage**, click **Groups**, and select the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-138">In the Azure Migrate project, under **Manage**, click **Groups**, and select the group.</span></span>
2. <span data-ttu-id="f65cd-139">On the group page, click **View Dependencies**, to open the group dependency map.</span><span class="sxs-lookup"><span data-stu-id="f65cd-139">On the group page, click **View Dependencies**, to open the group dependency map.</span></span>
3. <span data-ttu-id="f65cd-140">The dependency map for the group shows the following details:</span><span class="sxs-lookup"><span data-stu-id="f65cd-140">The dependency map for the group shows the following details:</span></span>
    - <span data-ttu-id="f65cd-141">Inbound (Clients) and outbound (Servers) TCP connections to/from all the machines that are part of the group</span><span class="sxs-lookup"><span data-stu-id="f65cd-141">Inbound (Clients) and outbound (Servers) TCP connections to/from all the machines that are part of the group</span></span>
        - <span data-ttu-id="f65cd-142">The dependent machines that do not have the MMA and dependency agent installed are grouped by port numbers</span><span class="sxs-lookup"><span data-stu-id="f65cd-142">The dependent machines that do not have the MMA and dependency agent installed are grouped by port numbers</span></span>
        - <span data-ttu-id="f65cd-143">The dependenct machines that have the MMA and the dependency agent installed are shown as separate boxes</span><span class="sxs-lookup"><span data-stu-id="f65cd-143">The dependenct machines that have the MMA and the dependency agent installed are shown as separate boxes</span></span> 
    - <span data-ttu-id="f65cd-144">Processes running inside the machine, you can expand each machine box to view the processes</span><span class="sxs-lookup"><span data-stu-id="f65cd-144">Processes running inside the machine, you can expand each machine box to view the processes</span></span>
    - <span data-ttu-id="f65cd-145">Properties like Fully Qualified Domain Name, Operating System, MAC Address etc. of each machine, you can click on each machine box to view these details</span><span class="sxs-lookup"><span data-stu-id="f65cd-145">Properties like Fully Qualified Domain Name, Operating System, MAC Address etc. of each machine, you can click on each machine box to view these details</span></span>

     ![View group dependencies](./media/how-to-create-group-dependencies/view-group-dependencies.png)

3. <span data-ttu-id="f65cd-147">To view more granular dependencies, click the time range to modify it.</span><span class="sxs-lookup"><span data-stu-id="f65cd-147">To view more granular dependencies, click the time range to modify it.</span></span> <span data-ttu-id="f65cd-148">By default, the range is an hour.</span><span class="sxs-lookup"><span data-stu-id="f65cd-148">By default, the range is an hour.</span></span> <span data-ttu-id="f65cd-149">You can modify the time range, or specify start and end dates, and duration.</span><span class="sxs-lookup"><span data-stu-id="f65cd-149">You can modify the time range, or specify start and end dates, and duration.</span></span>
4. <span data-ttu-id="f65cd-150">Verify the dependent machines, the process running inside each machine and identify the machines that should be added or removed from the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-150">Verify the dependent machines, the process running inside each machine and identify the machines that should be added or removed from the group.</span></span>
5. <span data-ttu-id="f65cd-151">Use Ctrl+Click to select machines on the map to add or remove them from the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-151">Use Ctrl+Click to select machines on the map to add or remove them from the group.</span></span>
    - <span data-ttu-id="f65cd-152">You can only add machines that have been discovered.</span><span class="sxs-lookup"><span data-stu-id="f65cd-152">You can only add machines that have been discovered.</span></span>
    - <span data-ttu-id="f65cd-153">Adding and removing machines from a group invalidates past assessments for it.</span><span class="sxs-lookup"><span data-stu-id="f65cd-153">Adding and removing machines from a group invalidates past assessments for it.</span></span>
    - <span data-ttu-id="f65cd-154">You can optionally create a new assessment when you modify the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-154">You can optionally create a new assessment when you modify the group.</span></span>
5. <span data-ttu-id="f65cd-155">Click **OK** to save the group.</span><span class="sxs-lookup"><span data-stu-id="f65cd-155">Click **OK** to save the group.</span></span>

    ![Add or remove machines](./media/how-to-create-group-dependencies/add-remove.png)

<span data-ttu-id="f65cd-157">If you want to check the dependencies of a specific machine that appears in the group dependency map, [set up machine dependency mapping](how-to-create-group-machine-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="f65cd-157">If you want to check the dependencies of a specific machine that appears in the group dependency map, [set up machine dependency mapping](how-to-create-group-machine-dependencies.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f65cd-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="f65cd-158">Next steps</span></span>

<span data-ttu-id="f65cd-159">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span><span class="sxs-lookup"><span data-stu-id="f65cd-159">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span></span>
