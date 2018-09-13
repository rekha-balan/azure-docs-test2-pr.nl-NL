---
title: Group machines using machine dependencies with Azure Migrate | Microsoft Docs
description: Describes how to create an assessment using machine dependencies with the Azure Migrate service.
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 07/05/2018
ms.author: raynew
ms.openlocfilehash: 4b83380558c10bc4f96d56f89a5cc2b7b53edc2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866131"
---
# <a name="group-machines-using-machine-dependency-mapping"></a><span data-ttu-id="2bce0-103">Group machines using machine dependency mapping</span><span class="sxs-lookup"><span data-stu-id="2bce0-103">Group machines using machine dependency mapping</span></span>

<span data-ttu-id="2bce0-104">This article describes how to create a group of machines for [Azure Migrate](migrate-overview.md) assessment by visualizing dependencies of machines.</span><span class="sxs-lookup"><span data-stu-id="2bce0-104">This article describes how to create a group of machines for [Azure Migrate](migrate-overview.md) assessment by visualizing dependencies of machines.</span></span> <span data-ttu-id="2bce0-105">You typically use this method when you want to assess groups of VMs with higher levels of confidence by cross-checking machine dependencies, before you run an assessment.</span><span class="sxs-lookup"><span data-stu-id="2bce0-105">You typically use this method when you want to assess groups of VMs with higher levels of confidence by cross-checking machine dependencies, before you run an assessment.</span></span> <span data-ttu-id="2bce0-106">Dependency visualization can help you effectively plan your migration to Azure.</span><span class="sxs-lookup"><span data-stu-id="2bce0-106">Dependency visualization can help you effectively plan your migration to Azure.</span></span> <span data-ttu-id="2bce0-107">It helps you ensure that nothing is left behind and surprise outages do not occur when you are migrating to Azure.</span><span class="sxs-lookup"><span data-stu-id="2bce0-107">It helps you ensure that nothing is left behind and surprise outages do not occur when you are migrating to Azure.</span></span> <span data-ttu-id="2bce0-108">You can discover all interdependent systems that need to migrate together and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.</span><span class="sxs-lookup"><span data-stu-id="2bce0-108">You can discover all interdependent systems that need to migrate together and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.</span></span>


## <a name="prepare-machines-for-dependency-mapping"></a><span data-ttu-id="2bce0-109">Prepare machines for dependency mapping</span><span class="sxs-lookup"><span data-stu-id="2bce0-109">Prepare machines for dependency mapping</span></span>
<span data-ttu-id="2bce0-110">To view dependencies of machines, you need to download and install agents on each on-premises machine that you want to evaluate.</span><span class="sxs-lookup"><span data-stu-id="2bce0-110">To view dependencies of machines, you need to download and install agents on each on-premises machine that you want to evaluate.</span></span> <span data-ttu-id="2bce0-111">In addition, if you have machines with no internet connectivity, you need to download and install [OMS gateway](../log-analytics/log-analytics-oms-gateway.md) on them.</span><span class="sxs-lookup"><span data-stu-id="2bce0-111">In addition, if you have machines with no internet connectivity, you need to download and install [OMS gateway](../log-analytics/log-analytics-oms-gateway.md) on them.</span></span>

### <a name="download-and-install-the-vm-agents"></a><span data-ttu-id="2bce0-112">Download and install the VM agents</span><span class="sxs-lookup"><span data-stu-id="2bce0-112">Download and install the VM agents</span></span>
1. <span data-ttu-id="2bce0-113">In **Overview**, click **Manage** > **Machines**, and select the required machine.</span><span class="sxs-lookup"><span data-stu-id="2bce0-113">In **Overview**, click **Manage** > **Machines**, and select the required machine.</span></span>
2. <span data-ttu-id="2bce0-114">In the **Dependencies** column, click **Install agents**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-114">In the **Dependencies** column, click **Install agents**.</span></span>
3. <span data-ttu-id="2bce0-115">On the **Dependencies** page, download and install the Microsoft Monitoring Agent (MMA), and the Dependency agent on each VM you want to evaluate.</span><span class="sxs-lookup"><span data-stu-id="2bce0-115">On the **Dependencies** page, download and install the Microsoft Monitoring Agent (MMA), and the Dependency agent on each VM you want to evaluate.</span></span>
4. <span data-ttu-id="2bce0-116">Copy the workspace ID and key.</span><span class="sxs-lookup"><span data-stu-id="2bce0-116">Copy the workspace ID and key.</span></span> <span data-ttu-id="2bce0-117">You need these when you install the MMA on the on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="2bce0-117">You need these when you install the MMA on the on-premises machine.</span></span>

> [!NOTE]
> <span data-ttu-id="2bce0-118">To automate the installation of agents you can use any deployment tool like System Center Configuration Manager or use our partner tool, [Intigua](https://www.intigua.com/getting-started-intigua-for-azure-migration), that has an agent deployment solution for Azure Migrate.</span><span class="sxs-lookup"><span data-stu-id="2bce0-118">To automate the installation of agents you can use any deployment tool like System Center Configuration Manager or use our partner tool, [Intigua](https://www.intigua.com/getting-started-intigua-for-azure-migration), that has an agent deployment solution for Azure Migrate.</span></span>

### <a name="install-the-mma"></a><span data-ttu-id="2bce0-119">Install the MMA</span><span class="sxs-lookup"><span data-stu-id="2bce0-119">Install the MMA</span></span>

<span data-ttu-id="2bce0-120">To install the agent on a Windows machine:</span><span class="sxs-lookup"><span data-stu-id="2bce0-120">To install the agent on a Windows machine:</span></span>

1. <span data-ttu-id="2bce0-121">Double-click the downloaded agent.</span><span class="sxs-lookup"><span data-stu-id="2bce0-121">Double-click the downloaded agent.</span></span>
2. <span data-ttu-id="2bce0-122">On the **Welcome** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-122">On the **Welcome** page, click **Next**.</span></span> <span data-ttu-id="2bce0-123">On the **License Terms** page, click **I Agree** to accept the license.</span><span class="sxs-lookup"><span data-stu-id="2bce0-123">On the **License Terms** page, click **I Agree** to accept the license.</span></span>
3. <span data-ttu-id="2bce0-124">In **Destination Folder**, keep or modify the default installation folder > **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-124">In **Destination Folder**, keep or modify the default installation folder > **Next**.</span></span>
4. <span data-ttu-id="2bce0-125">In **Agent Setup Options**, select **Azure Log Analytics** > **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-125">In **Agent Setup Options**, select **Azure Log Analytics** > **Next**.</span></span>
5. <span data-ttu-id="2bce0-126">Click **Add** to add a new Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="2bce0-126">Click **Add** to add a new Log Analytics workspace.</span></span> <span data-ttu-id="2bce0-127">Paste in the workspace ID and key that you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="2bce0-127">Paste in the workspace ID and key that you copied from the portal.</span></span> <span data-ttu-id="2bce0-128">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-128">Click **Next**.</span></span>


<span data-ttu-id="2bce0-129">To install the agent on a Linux machine:</span><span class="sxs-lookup"><span data-stu-id="2bce0-129">To install the agent on a Linux machine:</span></span>

1. <span data-ttu-id="2bce0-130">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span><span class="sxs-lookup"><span data-stu-id="2bce0-130">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
2. <span data-ttu-id="2bce0-131">Install the bundle by using the --install argument.</span><span class="sxs-lookup"><span data-stu-id="2bce0-131">Install the bundle by using the --install argument.</span></span>

    ```sudo sh ./omsagent-<version>.universal.x64.sh --install -w <workspace id> -s <workspace key>```


### <a name="install-the-dependency-agent"></a><span data-ttu-id="2bce0-132">Install the Dependency agent</span><span class="sxs-lookup"><span data-stu-id="2bce0-132">Install the Dependency agent</span></span>
1. <span data-ttu-id="2bce0-133">To install the Dependency agent on a Windows machine, double-click the setup file and follow the wizard.</span><span class="sxs-lookup"><span data-stu-id="2bce0-133">To install the Dependency agent on a Windows machine, double-click the setup file and follow the wizard.</span></span>
2. <span data-ttu-id="2bce0-134">To install the Dependency agent on a Linux machine, install as root using the following command:</span><span class="sxs-lookup"><span data-stu-id="2bce0-134">To install the Dependency agent on a Linux machine, install as root using the following command:</span></span>

    ```sh InstallDependencyAgent-Linux64.bin```

<span data-ttu-id="2bce0-135">Learn more about the Dependency agent support for the [Windows](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) and [Linux](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) operating systems.</span><span class="sxs-lookup"><span data-stu-id="2bce0-135">Learn more about the Dependency agent support for the [Windows](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) and [Linux](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) operating systems.</span></span>

<span data-ttu-id="2bce0-136">[Learn more](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure#installation-script-examples) about how you can use scripts to install the Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="2bce0-136">[Learn more](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure#installation-script-examples) about how you can use scripts to install the Dependency agent.</span></span>

## <a name="create-a-group"></a><span data-ttu-id="2bce0-137">Create a group</span><span class="sxs-lookup"><span data-stu-id="2bce0-137">Create a group</span></span>

1. <span data-ttu-id="2bce0-138">After you install the agents, go to the portal and click **Manage** > **Machines**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-138">After you install the agents, go to the portal and click **Manage** > **Machines**.</span></span>
2. <span data-ttu-id="2bce0-139">Search for the machine where you installed the agents.</span><span class="sxs-lookup"><span data-stu-id="2bce0-139">Search for the machine where you installed the agents.</span></span>
3. <span data-ttu-id="2bce0-140">The **Dependencies** column for the machine should now show as **View Dependencies**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-140">The **Dependencies** column for the machine should now show as **View Dependencies**.</span></span> <span data-ttu-id="2bce0-141">Click the column to view the dependencies of the machine.</span><span class="sxs-lookup"><span data-stu-id="2bce0-141">Click the column to view the dependencies of the machine.</span></span>
4. <span data-ttu-id="2bce0-142">The dependency map for the machine shows the following details:</span><span class="sxs-lookup"><span data-stu-id="2bce0-142">The dependency map for the machine shows the following details:</span></span>
    - <span data-ttu-id="2bce0-143">Inbound (Clients) and outbound (Servers) TCP connections to/from the machine</span><span class="sxs-lookup"><span data-stu-id="2bce0-143">Inbound (Clients) and outbound (Servers) TCP connections to/from the machine</span></span>
        - <span data-ttu-id="2bce0-144">The dependent machines that do not have the MMA and dependency agent installed are grouped by port numbers</span><span class="sxs-lookup"><span data-stu-id="2bce0-144">The dependent machines that do not have the MMA and dependency agent installed are grouped by port numbers</span></span>
        - <span data-ttu-id="2bce0-145">The dependent machines that have the MMA and the dependency agent installed are shown as separate boxes</span><span class="sxs-lookup"><span data-stu-id="2bce0-145">The dependent machines that have the MMA and the dependency agent installed are shown as separate boxes</span></span>
    - <span data-ttu-id="2bce0-146">Processes running inside the machine, you can expand each machine box to view the processes</span><span class="sxs-lookup"><span data-stu-id="2bce0-146">Processes running inside the machine, you can expand each machine box to view the processes</span></span>
    - <span data-ttu-id="2bce0-147">Properties like Fully Qualified Domain Name, Operating System, MAC Address etc. of each machine, you can click on each machine box to view these details</span><span class="sxs-lookup"><span data-stu-id="2bce0-147">Properties like Fully Qualified Domain Name, Operating System, MAC Address etc. of each machine, you can click on each machine box to view these details</span></span>

 ![View machine dependencies](./media/how-to-create-group-machine-dependencies/machine-dependencies.png)

4. <span data-ttu-id="2bce0-149">You can look at dependencies for different time durations by clicking on the time duration in the time range label.</span><span class="sxs-lookup"><span data-stu-id="2bce0-149">You can look at dependencies for different time durations by clicking on the time duration in the time range label.</span></span> <span data-ttu-id="2bce0-150">By default the range is an hour.</span><span class="sxs-lookup"><span data-stu-id="2bce0-150">By default the range is an hour.</span></span> <span data-ttu-id="2bce0-151">You can modify the time range, or specify start and end dates, and duration.</span><span class="sxs-lookup"><span data-stu-id="2bce0-151">You can modify the time range, or specify start and end dates, and duration.</span></span>
5. <span data-ttu-id="2bce0-152">After you've identified dependent machines that you want to group together, use Ctrl+Click to select multiple machines on the map, and click **Group machines**.</span><span class="sxs-lookup"><span data-stu-id="2bce0-152">After you've identified dependent machines that you want to group together, use Ctrl+Click to select multiple machines on the map, and click **Group machines**.</span></span>
6. <span data-ttu-id="2bce0-153">Specify a group name.</span><span class="sxs-lookup"><span data-stu-id="2bce0-153">Specify a group name.</span></span> <span data-ttu-id="2bce0-154">Verify that the dependent machines are discovered by Azure Migrate.</span><span class="sxs-lookup"><span data-stu-id="2bce0-154">Verify that the dependent machines are discovered by Azure Migrate.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2bce0-155">If a dependent machine is not discovered by Azure Migrate, you cannot add it to the group.</span><span class="sxs-lookup"><span data-stu-id="2bce0-155">If a dependent machine is not discovered by Azure Migrate, you cannot add it to the group.</span></span> <span data-ttu-id="2bce0-156">To add such machines to the group, you need to run the discovery process again with the right scope in vCenter Server and ensure that the machine is discovered by Azure Migrate.</span><span class="sxs-lookup"><span data-stu-id="2bce0-156">To add such machines to the group, you need to run the discovery process again with the right scope in vCenter Server and ensure that the machine is discovered by Azure Migrate.</span></span>  

7. <span data-ttu-id="2bce0-157">If you want to create an assessment for this group, select the checkbox to create a new assessment for the group.</span><span class="sxs-lookup"><span data-stu-id="2bce0-157">If you want to create an assessment for this group, select the checkbox to create a new assessment for the group.</span></span>
8. <span data-ttu-id="2bce0-158">Click **OK** to save the group.</span><span class="sxs-lookup"><span data-stu-id="2bce0-158">Click **OK** to save the group.</span></span>

<span data-ttu-id="2bce0-159">Once the group is created, it is recommended to install agents on all the machines of the group and refine the group by visualizing the dependency of the entire group.</span><span class="sxs-lookup"><span data-stu-id="2bce0-159">Once the group is created, it is recommended to install agents on all the machines of the group and refine the group by visualizing the dependency of the entire group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bce0-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="2bce0-160">Next steps</span></span>

- <span data-ttu-id="2bce0-161">[Learn how](how-to-create-group-dependencies.md) to refine the group by visualizing group dependencies</span><span class="sxs-lookup"><span data-stu-id="2bce0-161">[Learn how](how-to-create-group-dependencies.md) to refine the group by visualizing group dependencies</span></span>
- <span data-ttu-id="2bce0-162">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span><span class="sxs-lookup"><span data-stu-id="2bce0-162">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span></span>
